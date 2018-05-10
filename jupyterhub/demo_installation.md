# Demo setup for Jupyterhub / nbgrader

**This installation recipe comes without any warranty. Backup first!**

* install the Anaconda distribution to /opt/anaconda3
* install jupyterhub    
    * prerequisites   
     `sudo apt-get install npm nodejs`   
     `npm install -g configurable-http-proxy`
     
    * create self-signed TLS certificate and move it to correct system directory   
     `openssl req -new -newkey rsa:4096 -x509 -sha256 -days 365 -nodes -out jupyterhub.crt -keyout jupyterhub.key`    
     `sudo mv jupyterhub.crt /etc/ssl/certs/`   
     `sudo mv jupyterhub.key /etc/ssl/private/`   
     `sudo ls -l /etc/ssl/private/jupyterhub.key`

    * conda install   
      `sudo /opt/anaconda3/bin/conda install -c conda-forge jupyterhub`   
      `sudo /opt/anacodna3/bin/conda install notebook`

    * create config   
      `sudo mkdir /etc/jupyterhub`   
      `sudo /opt/anaconda3/bin/jupyterhub --generate-config -f /etc/jupyterhub/jupyterhub_config.py`   
      and adapt:   
      `c.JupyterHub.cookie_secret_file = '/srv/jupyter/jupyterhub_cookie_secret'`   
      `c.JupyterHub.db_url = '/srv/jupyter/jupyterhub.sqlite'`   
      `c.JupyterHub.ssl_cert = '/etc/ssl/certs/jupyterhub.crt'`   
      `c.JupyterHub.ssl_key = '/etc/ssl/private/jupyterhub.key'`   
      `c.Spawner.cmd = ['/opt/anaconda3/bin/jupyterhub-singleuser']`   
      `c.PAMAuthenticator.service = 'login'`   

    * set up directory for jupyterhub database
      `mkdir -p /srv/jupyterhub`

* install nbgrader    
  `sudo /opt/anaconda3/bin/conda install -c conda-forge nbgrader`   
  `sudo /opt/anaconda3/bin/jupyter nbextension install --sys-prefix --py nbgrader --overwrite`   
  `sudo /opt/anaconda3/bin/jupyter nbextension enable --sys-prefix --py nbgrader`
  `sudo /opt/anaconda3/bin/jupyter serverextension enable --sys-prefix --py nbgrader`

* set up nbgrader    
  `sudo mkdir -p /srv/nbgrader/exchange`
  `sudo chmod 777 /srv/nbgrader/exchange`

* set up instructor account    
  `sudo adduser instructor`

* set up test course   
  `mkdir nbgrader`   
  `cd nbgrader`
  `nbgrader quickstart testcourse`   
  create directory `.jupyter` if it does not exist already   
  `mkdir ~/.jupyter`   
  add configuration file `~/.jupyter/nbgrader_config.py` containing the following lines    
```
    c = get_config()
    c.Exchange.course_id = 'testcourse'
    c.CourseDirectory.root = '/home/instructor/nbgrader/testcourse'
```

* set up student account   
  `sudo adduser student`
  
* run jupyterhub   
  `sudo /opt/anaconda3/bin/jupyterhub -f /etc/jupyterhub/jupyterhub_config.py`
