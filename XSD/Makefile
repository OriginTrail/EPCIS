# run xmllint schema validation test on all xml files

# make sure xmllint is avaible
ifeq (, $(shell which xmllint))
 $(error "no xmllint in $(PATH), xmllint is required to run validation")
 endif

all : valid
.PHONY : all

# xml files to be tested
EVENT_XMLS:=$(wildcard ../XML/*.xml) $(wildcard ../XML/*Event*/*.xml) $(wildcard ../XML/With*/*.xml) $(wildcard ../XML/Mimasu/Example?.xml) $(wildcard ../XML/Mimasu/*Event*.xml)

VOCABULARY_XMLS:=$(wildcard ../XML/CBV/*.xml) $(wildcard ../XML/Mimasu/*masterData.xml)

CAPTURE_XMLS:=$(wildcard ../XML/CaptureJob/*.xml)

# create tests from filenames
EVENT_XMLTESTS:=$(patsubst %.xml,%.event-test,$(EVENT_XMLS))
VOCABULARY_XMLTESTS:=$(patsubst %.xml,%.vocabulary-test,$(VOCABULARY_XMLS))
CAPTURE_XMLTESTS:=$(patsubst %.xml,%.capture-test,$(CAPTURE_XMLS))

valid-events: $(EVENT_XMLTESTS)
valid-vocabulary: $(VOCABULARY_XMLTESTS)
valid-capture: $(CAPTURE_XMLTESTS)

valid: valid-events valid-vocabulary valid-capture

# prepare XML Schema 1.0 by relaxing Schema 1.1 definitions
#prepare:
#	mkdir tmp; find ./ -name '*.xsd' -maxdepth 1 -exec sh -c 'sed "s/xsd\:dateTimeStamp/xsd:\dateTime/g"  {} > tmp/{}' \;

#clean:
#	rm -Rf tmp;

# Each test depends on the XML file
# Now we have a pattern on both sides of the generic rule
%.event-test: %.xml
	xmllint --noout --schema EPCglobal-epcis-2_0_alt.xsd  $<

%.vocabulary-test: %.xml
	xmllint --noout --schema EPCglobal-epcis-masterdata-2_0_alt.xsd  $<

%.capture-test: %.xml
	xmllint --noout --schema EPCglobal-epcis-2_0_alt.xsd  $<	