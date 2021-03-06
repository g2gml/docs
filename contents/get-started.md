# Quick Start

## Sandbox

To understand how G2GML works quickly, please visit the sandbox.

* [http://purl.org/g2gml](http://purl.org/g2gml)

Some usage samples are provided.
Notice that in order to use the sandbox effectively, knowledge about RDF and SPARQL are strongly recommended.

## Command Line Usage

### Installation

Set an alias to run a docker container:

    $ alias g2g='docker run --rm -v $PWD:/work g2glab/g2g:0.3.5 g2g'

Check if it works:

    $ g2g --help

### Execution

Download example turtle file:

    $ wget https://raw.githubusercontent.com/g2glab/g2g/master/examples/mini-05/mini-05.ttl
    
`mini-05.ttl`
    
    @prefix : <http://example.org/> .
    :person1 a :Person .
    :person2 a :Person .
    [] a :Follow ;
       :follower :person1 ;
       :followed :person2 ;
       :since 2017 .
    
Download example g2g file:

    $ wget https://raw.githubusercontent.com/g2glab/g2g/master/examples/mini-05/mini-05.g2g
    
`mini-05.g2g`

    PREFIX : <http://example.org/>
    
    (p:person)
        ?p a :Person .
    
    (p1:person)-[:follows {since:s}]->(p2:person)
        ?f :follower ?p1 ;
           :followed ?p2 ;
           :since ?s .

Run (mapping against RDF data file):

    $ g2g mini-05.g2g mini-05.ttl

Check the output file:

    $ more output/mini-05/mini-05.pg

`mini-05.pg`

    "http://example.org/person1" :person
    "http://example.org/person2" :person
    "http://example.org/person1" -> "http://example.org/person2" :follows since:2017

For further details please refer to:

* [G2GML](https://g2gml.readthedocs.io/en/latest/contents/g2gml.html): Description of the mapping language.
* [G2G Mapper](https://g2gml.readthedocs.io/en/latest/contents/g2g-mapper.html): Usage of the command line tool.

## Related tools

* [PG Tools](https://pg-format.readthedocs.io/en/latest/): Tools to manage resulting property graph files.
