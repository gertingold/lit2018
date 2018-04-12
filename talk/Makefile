_imgdownload = eu_flag_co_funded_pos_[rgb]_right.jpg

eu_flag_co_funded_pos_[rgb]_right.jpg:
	wget http://eacea.ec.europa.eu/img/logos/erasmus_plus/eu_flag_co_funded_pos_%5Brgb%5D_right.jpg

all: lit2018.tex $(_imgdownload)
	pdflatex lit2018.tex
	pdflatex lit2018.tex

clean:
	-rm lit2018.aux lit2018.log lit2018.nav lit2018.out \
	    lit2018.snm lit2018.pdf lit2018.toc \
	    $(_imgdownload)
