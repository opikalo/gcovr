all:
	$(CXX) -fprofile-arcs -ftest-coverage -fPIC main.cpp -o testcase

run: txt xml html sonarqube json json_summary

txt:
	./testcase
	$(GCOVR) -d -o coverage.txt

xml:
	./testcase
	$(GCOVR) -d -x -o coverage.xml

html:
	./testcase
	$(GCOVR) -d --html-details -o coverage.html

sonarqube:
	./testcase
	$(GCOVR) -d --sonarqube sonarqube.xml

json:
	# pass

json_summary:
	./testcase
	$(GCOVR) -d --json-summary --json-pretty -o summary_coverage.json

clean:
	rm -f testcase
	rm -f *.gc*
	rm -f coverage.txt coverage.xml coverage*.html sonarqube.xml summary_coverage.json
