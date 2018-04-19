.PHONY: all cleantex clean

_imgdownload = eu_flag_co_funded_pos_[rgb]_right.jpg python-logo-master-v3-TM.png \
               Top39-700_4.png sln_logo.png

all: lit2018.tex $(_imgdownload)
	pdflatex lit2018.tex
	pdflatex lit2018.tex

eu_flag_co_funded_pos_[rgb]_right.jpg:
	wget http://eacea.ec.europa.eu/img/logos/erasmus_plus/eu_flag_co_funded_pos_%5Brgb%5D_right.jpg

python-logo-master-v3-TM.png:
	wget https://www.python.org/static/community_logos/python-logo-master-v3-TM.png

Top39-700_4.png:
	wget https://cacm.acm.org/system/assets/0001/6722/Top39-700.4.png
	mv Top39-700.4.png Top39-700_4.png

sln_logo.svg:
	wget https://www.scipy-lectures.org/_images/logo.svg

sln_logo.png: sln_logo.svg
	inkscape -z -e sln_logo.png -w 1024 logo.svg

cleantex:
	rm lit2018.aux lit2018.log lit2018.nav lit2018.out \
	   lit2018.snm lit2018.toc lit2018.vrb

clean: cleantex
	rm $(_imgdownload)
	rm sln_logo.png
