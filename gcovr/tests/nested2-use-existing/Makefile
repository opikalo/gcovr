CFLAGS= -fprofile-arcs -ftest-coverage -fPIC
GCOV ?= gcov

export GCOV

all:
	make -C subdir/A
	$(CXX) $(CFLAGS) -c subdir/B/main.cpp -o subdir/B/main.o
	$(CXX) $(CFLAGS) subdir/B/main.o subdir/A/file1.o subdir/A/file2.o subdir/A/file3.o subdir/A/file4.o subdir/A/C/file5.o subdir/A/C/D/file6.o subdir/A/file7.o  -o subdir/B/testcase -lgcov

run: txt xml html sonarqube json json_summary

txt:
	./subdir/B/testcase
	make -C subdir/A coverage
	$(GCOV) --branch-counts --branch-probabilities --preserve-paths subdir/B/main.o
	$(GCOVR) -r subdir -g -k -o coverage.txt .

# this test also includes a separator "--"
# to ensure that nargs=? arguments can be terminated
xml:
	./subdir/B/testcase
	make -C subdir/A coverage
	$(GCOV) --branch-counts --branch-probabilities --preserve-paths subdir/B/main.o
	$(GCOVR) -r subdir -g -k -o coverage.xml -x -- .

html:
	./subdir/B/testcase
	make -C subdir/A coverage
	$(GCOV) --branch-counts --branch-probabilities --preserve-paths subdir/B/main.o
	$(GCOVR) -r subdir -g -k --html-details -o coverage.html .

sonarqube:
	./subdir/B/testcase
	make -C subdir/A coverage
	$(GCOV) --branch-counts --branch-probabilities --preserve-paths subdir/B/main.o
	$(GCOVR) -r subdir -g -k --sonarqube sonarqube.xml .

json:
	# pass

json_summary:
	# pass

clean:
	rm -f ./subdir/B/testcase subdir/lib.a
	rm -f *.gc* */*.gc* */*/*.gc* */*/*/*.gc* */*/*/*/*.gc*
	rm -f *.o */*.o */*/*.o */*/*/*.o */*/*/*/*.o
	rm -f coverage.txt coverage.xml coverage*.html sonarqube.xml
