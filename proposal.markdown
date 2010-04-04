Proposal for PDB-Tidy: A Command-line tool for manipulating PDB files.
======================================================================

1.- About the student.
-----------------------

  My name is Carlos Ríos, I'm from Concepción, Chile. I'm a Technical Engineer
in Computer Sciences student at [Universidad del Bío-Bio][1]. Currently I'm on
my fourth year and I expect to graduate by the first half of 2011.

I'm particularly interested in bioinformatics. Since last year, I have been
involved in several projects at the Molecular Biophysics Lab at the [Universidad
de Concepción][2], doing software development tasks as an intern. Here I realise
that this field -bioinformatics- is where I have to stay. I have also taken the
bioinformatic class the last semester, and this semester I will take a
biochemestry class.

My interest in FLOSS began when I was at primary school and one of our teachers
showed us Mandrake Linux. Since then, I'm an active Linux user and also an
organizer of ["Encuentro Linux"][3] (one of largest Linux conferences in the
country). I have also given some talks in other universities and institutes
about the Linux Terminal Server Project like a alternative to use the old
machines in Public Schools where the technological investment is very poor, and
also other talks about the use of FLOSS.



2.- About the student's skills.
--------------------------------

  I consider myself as a programmer who love to learn new staff, for that
reason I want to be a bioinformatitian.

The programming languages that I feel very confortable are: Python and C, but I
can code in: PHP, C++, Java.

In my workstation and house-station I use GNU/Linux (sometimes a *BSD flavour),
so as you can see I have experience in the use of Unix likes systems.

For web developing I use Python and the [webpy][3] framework, In my time in the
lab as intern, I had to work with python and the Biopython module,
besides I used PyMol (as a GUI tool and as python module). I have also
contributed in the PyMol package distributed by the linux distro that I use.

About authored or contributed FLOSS project, in my lab we started a new project
named VisualDEP, which should be a service released as a GPLv2 software. In this
project we use several tools (PyMol, Biopython, pdb2pqr, APBS). So I can say
that I have experience working with PDB files.

As you can see in my [blog][4] I love programming.



3.- About the project-idea you want propose.
---------------------------------------------

### 3.1.- Name of the idea:
  [PDB-Tidy: A Command-line tool for manipulating PDB files.][5] Based on the idea
proposed by the mentor [Eric Talevich][6].


### 3.2.- Programming language:
  Python + Biopython module.


### 3.3.- Abstract:

  We know that the Protein Data Bank and its PDB file format offers a huge
amount of data that sometimes structural biologists can't handle easily and the
currently available tools for work on it are usually specialized for a single
specific task (e.g. visualization, homology modelling). For that reason we
introduce PDB-Tidy which is a Command Line tool and a Biopython module as well.
PDB-Tidy enables you to perform PDB handling in a easy way (e.g. renumber
residues), all in one package, you don't have to use several tools to perform
a single target.


### 3.4.- List of features:

#### a) Renumber residues starting from 1 (or N).
  When preparing structures for modeling or simulations, and sometimes
when working with sequence alignments, it's useful to choose the
starting residue numbers. Also, some PDB files are not numbered
sequentially, so this can correct such files even without changing the
starting residue number.

#### b) Transform the PDB file into other formats supported by biopython.
  The SeqIO module supports a large range of formats, PDB-Tidy will
enable the convertion from PDB to those formats that SeqIO supports.

#### c) Read the PDB File and return information about the aminoacidic composition and the molecular weight.
  For some experiments is very useful this information.
e.g. SDS-PAGE analisys.

#### d) Check for incomplete amino acids.
<br />

#### e) Rename protein chains.
<br />

#### f) Split a chain or PDB file by adding the corresponding terminal oxigen.
<br />

#### g) Change the B-factor value for other scales like charge, exposition, hydrophobicity; for then paint them in visualization tools.
  Some experiments sometimes has the need to add a new scale of values
by atom or residue, change the B-factor value by those values is a good
alternative to display them in visualization tools.

#### h) In high resolution structures, with B-factor refinement, the anisotropic values (6 values) transform them into one value.
<br />

#### i) Selecting an amino acid, show the neighbors in xÅ of it.
  The knowledge of the neighbors of an amino acid can help to know in
what environment is acting.

#### j) Generate a ramachandran plot of the protein.


*All these features will be available as command tool and as Biopython module.*


### 3.5.- Brief example of the use of PDB-Tidy:

#### a) Renumber residues starting from 1 (or N):
#####  a.1) As coommand tool:
    % ls
        1eyx.pdb
    % PDBTidy renumber --start=53 --chain=A -i 1eyx.pdb -o 1eyx_.pdb
    % ls
        1eyx.pdb    1eyx_.pdb

   -Ommiting the `--start` argument, it will use 1 as default value.

   -Ommiting the `--chain` argument, the renumber function will act over all the
   chains.

   -Ommiting the `-i` argument, the tool will use `stdin` (or `pipe`) to get the
   data. Example:

    % cat 1eyx.pdb | PDBTidy renumber -o 1eyx_.pdb

   -Ommiting the `-o` argument, the tool will use `stdout`. Example:

    % PDBTidy renumber -i 1eyx.pdb > 1eyx_.pdb


##### a.2) As Biopython module:
    >>> import Bio
    >>> parser = Bio.PDB.PDBParser()
    >>> structure = parser.get_structure("1EYX", "1eyx.pdb")
    >>> ns = Bio.PDB.PDBTidy.renum_residues(structure, X)
    >>> io = Bio.PDB.PDBIO()
    >>> io.set_structure(ns)
    >>> io.save("1eyx_.pdb")

#### b) Transform the PDB file into other format (e.g. fasta, pir):
#####  b.1) As command tool:
    % ls
        1eyx.pdb    1eyx_.pdb
    % PDBTidy getsequence --format fasta -i 1eyx_.pdb > 1eyx_.fasta
    %ls
        1eyx.pdb    1eyx_.fasta    1eyx_.pdb

   -You can add the `--chain` argument to extract a specific chain.


#####  b.2) As Biopython module:
    >>> import Bio
    >>> parser = Bio.PDB.PDBParser()
    >>> structure = parser.get_structure("1EYX", "1eyx_.pdb")
    >>> nf = Bio.PDB.PDBTidy.get_sequence(structure, format="fasta")
    >>> f = open("1eyx_.fasta", "w")
    >>> f.writelines( nf )
    >>> f.close()

   As you can see PDB-Tidy is a sub-module that is included in the Bio.PDB
   module.


### 3.6.- Other information about the idea:

  The PDB-Tidy code will be released with the Biopython licence. In the
development of the software I will use [GitHub][7] to have the code into a
public repository.



4.- Project schedule.
----------------------

  This schedule was made according the official Google Summer of Code
schedule.

#### April 26 - May 23:
#####  Tasks: 
-    Collect PDB files that represent the future use cases e.g. PDB
     files with incomplete amino acids.
-    Read documentation about biopython modules involved in the PDB-Tidy
     construction (Bio.PDB, Bio.SeqIO).
-    Get in touch with the mentors and the biopython community to get
     feedback from them.


#### May 24 - June 7:
#####  Tasks: - Implement the 'renumber residues' feature [a] (see section 3.4).
-    Implement the 'transform PDB to other format' feature [b] (see
     section 3.4).
-    Implement the 'return amino acid composition and molecular weight'
     feature [c] (see section 3.4).

#####  Goals:
-    Features a, b, c released (see above).
-    Unit test for features a, b & c.


#### June 8 - 21:
#####  Tasks:
-    Write documentation for a, b & c features.
-    Implement the 'check for incomplete residues' feature [d] (see
     section 3.4).
-    Implement the 'rename protein chains' feature [e] (see section 3.4)
-    Implement the 'split chains by adding the terminal oxygen' feature
     [f] (see section 3.4).

#####  Goals: - Features d, e, f released (see above).
-    Unit test for features d, e & f.
-    Documentation for features a, b & c.


#### June 22 - July 5:
#####  Tasks:
-    Write documentation for d, e & f features.
-    Implement the 'change B-factor value for other scale' feature [g]
     (see section 3.4).
-    Implement the 'transform the anisotropic b-factor to isotropic'
     feature [h] (see section 3.4).
-    Implement the 'show the neighbors from a selected residue' feature
     [i] (see section 3.4).

#####  Goals: - Features g, h, i released (see above).
-    Unit test for features g, h & i.
-    Documentation for features d, e & f.


#### July 12-16:
#####  Tasks:
-    Working with the mentor in the evaluations.


#### July 6-26:
#####  Tasks: 
-    Write documentation for g, h & features.
-    Implement the 'generate a ramachandran plot of the protein' feature
     [j] (see section 3.4).

#####  Goals:
-    Feature j released (see above).
-    Unit test for feature j.
-    Documentation for features g, h & i.


#### July 27 - August 2:
#####  Tasks:
-    Write documentation for i feature.

#####  Goals:
-    Documentation for i feature.


#### August 3-15: 
#####  Tasks:
-    Get feedback from the community.
-    Identify bugs.

#####  Goals:
-    Patches for fix bugs in the software and documentation.


#### August 16-20:
#####  Tasks:
-    Working with the mentor in the final evaluation.




5.- Feedback:
--------------

  Any question, comment or dissagreement? Don't doubt and send me an e-mail
to: crosvera at gmail dot com. You can also find me on IRC at irc.freenode.net
and irc.cl as crosvera.


[1]: http://www.ubiobio.cl

[2]: http://www.udec.cl

[3]: http://www.encuentrolinux.cl

[4]: http://crosvera.blogspot.com

[5]: http://biopython.org/wiki/Google_Summer_of_Code#PDB-Tidy:_command-line_tools_for_manipulating_PDB_files

[6]: http://biopython.org/wiki/User:EricTalevich

[7]: http://www.github.com


