

# An Open Source PageRank Implementation

This project provides an open source PageRank implementation. The
implementation is a straightforward application of the algorithm
description given in the American Mathematical Society's Feature
Column.

# Building

The project is written in standard C++ and can be built by running:

    g++ -o pagerank pagerank.cpp table.cpp table.h

# Usage

pagerank is invoked by

    pagerank [OPTIONS] graph_file

where OPTIONS may be:

* -t: if set, tracing is enabled. Tracing outputs all intermediate
   steps of the pagerank calculation algorithm and can be very
   voluminous.

* -n: if set, the graph_file is in numeric format, that is it consists
   of lines of the form `<from><delim><to>` where `<from>` and `<to>` are
   integer vertex indices, starting with zero. If not set, the
   graph_file consists of lines of the form `<from><delim><to>` where
   `<from>` and `<to>` are vertex IDs that will be interpreted as strings.

* -a `<float>`: the pagerank dumping factor; default is  0.85.

* -c `<float>`: the convergence criterion. The pagerank iterations will
   stop when two successive iterations have converged to less than or
   equal to this value. Default is 0.00001.

* -s `<integer>`: the number of rows of the hyperlink matrix. This is
   not the maximum size; if the graph requires more rows, they will be
   allocated as necessary. If an approximate size is known beforehand,
   however, the necessary internal data structures can be
   pre-allocated for better performance.

* -d `<string>`: the delimited used to separate vector indices in the
   input graph file. Default is `" => "`.



The test driver is written in standard C++ and can be compiled with:

    g++ -I../cpp -o pagerank_test pagerank_test.cpp ../cpp/table.cpp 


# C++ implementation of hubs and authorities (HITS) and PageRank algorithms


#### Building
If you are building from this repository you will need to do the standard things:

* aclocal
* autoconf
* automake
* ./configure
* make

#### Example

The examples folder contains citation graph for an ant specimen and various entities (DNA sequences, images, publications) that "cite" that specimen:



Running the program on this graph

* matching examples/CASENT0106070.gml

produces a text dump of PageRank values.

	Graph read from file "examples/CASENT0106070.gml" has 10 nodes and 20 edges
	Node	Page rank
	CASENT0106070	1.25722
	AY703487	0.194147
	AY703554 	0.194147
	AY703621 	0.194147
	AY703688	0.194147
	AY703755 	0.194147
	EF013219	0.165938
	EF013381	0.165938
	doi:10.1111/j.1365-3113.2004.00281.x	0.165938
	pmdi:17079492	0.15


