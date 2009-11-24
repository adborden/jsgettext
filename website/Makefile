.PHONY: all clean install

SOURCE=../lib/Gettext.js
PO2JSONSOURCE=../bin/po2json
DEMO=../examples/normal/index.html
PREFIX?=/home/groups/jsgettext

TEST_FILES:=$(shell find ../tests -path "*/CVS" -prune -o ! -name ".*" -print)

all:htdocs/doc/html/Gettext.html htdocs/doc/html/po2json.html \
	htdocs/lib/Gettext.js htdocs/demo/index.html htdocs/tests

install: $(PREFIX) all
	find htdocs -path "*/CVS" -prune -o ! -name ".*" -print | \
	cpio -o | \
	(cd $< ; cpio -iu )

htdocs/tests: $(TEST_FILES)
	mkdir -p $@
	cd ../ && \
	find tests -path "*/CVS" -prune -o ! -name ".*" -print | \
	cpio -o | \
	(cd website/htdocs && cpio -iu )

htdocs/lib/Gettext.js: $(SOURCE) htdocs/lib
	cp $< $@

htdocs/doc/html/Gettext.html: $(SOURCE) htdocs/doc/html
	pod2html $< > $@
	rm pod2htm*.tmp

htdocs/doc/html/po2json.html: $(PO2JSONSOURCE) htdocs/doc/html
	pod2html $< > $@
	rm pod2htm*.tmp

htdocs/demo/index.html: $(DEMO) htdocs/demo
	cat $< | sed 's/..\/..\/lib\/Gettext.js/..\/lib\/Gettext.js/' > $@

htdocs/doc/html htdocs/demo htdocs/lib:
	mkdir -p $@

clean:
	rm -fr htdocs/lib
	rm -fr htdocs/doc
	rm -fr htdocs/demo
	rm -fr htdocs/tests

