Tutorial 

(1)Cloning and installing the repositories 
 1. Readers should make sure to have Python 3 and git installed on the computer.
  If so, open a git-enabled Terminal window or command line.
  
 2. Even though it is not required, we recommend the readers create a new Python virtual environment for the following process,
  as a few packages will be installed. New python virtual environment can be done anywhere and the command line can be found at <https://docs.python.org/3/library/venv.html>
  
 3. Once the virtual environment is created, type or paste the following command: <git clone https://github.com/lexibank/deepadungpalaung.git.>
 This will create a directory named <deepadungpalaung/> in the current working directory containing a copy of the repository.
 
 4. Next, type the following command: <pip install -e deepadungpalaung>
 This command installs within the virtual environment all the packages necessary for using the repository. This process should take several minutes. 
 
 5. After all the preparation is done,type or paste the following command:<git clone https://github.com/Juunlee/Palaung\_scripts.git>
 This will create a folder that includes the python files needed for automatic phylogeny.

(2)Running the scripts 

 6. Navigate into the <Palaung\_scripts/> directory by typing the following command:<cd Palaung\_scripts>.
 Now type in the following command to execute the cognate detection script: <python cognate\_detection.py>. 
 When the program starts running, it will require readers to choose which algorithm to use to do automated cognate detection. 
 Readers should type any of the following four possibilities: <lexstatcogids> <lexstatcogid> <scacogids> <scacogid>.
 It doesn't matter where this directory is relative to the <deepadungpalaung/> directory, since it uses <lexibank\_deepadungpalaung.Dataset> to know where <deepadungpalaung/> is on the computer.
 
 7. Then <cognate\_detection.py> will display a phylogenetic tree in your terminal and create a separate distance matrix csv in the <output/> directory under <deepadungpalaung>. 
 For instance, if you choose 'lexstatcogids', it will create <deepadungpalaung/output/distmat\_lexstatcogids.csv>.
 
 8. This distance matrix created by the program can be turned into a tree by using two methods. 
 First, readers can open the csv in a text editor and paste it as text into DendroUPGMA at <http://genomes.urv.cat/UPGMA/> choosing option (c) a distance matrix. 
 This decorates an internal node with the distance to any of its leaves, and was the method used to generate the images in this paper.
 
 9. The second method is by using the <UPGMA.p> in the <Palaung\_scripts/> directory.
  In the terminal, type the following command: <python UPGMA.py>. Then, type the same method that was used to create the distance matrix.
  
 10. This method will create a file in <deepadungpalaung/output/> called <tree\_lexstatcogids.xml> (in the case of lexstatcogids), which
 can then be opened in a web browser to see internal nodes decorated with the average distance between the two groups joined. 
 Note that this number would be greater than the number given by the tree display in step 8.
 
(3)Editing orthography.tsv and remaking the CLDF

 11. By editing the <orthography.tsv>, users can divide words into different partial segments. 
 In the first column of the <orthography.tsv> , users input the letters that will be changed. 
 Then, using tab, users can write down the change they want to make in the second column.
 
 12. If the user inputs <әh> and writes down <ә h>, these two letters will be displayed as separated in <deepadungpalaung/cldf/forms.csv>.
 
 13.  After editing the <orthography.tsv>, open a git-enabled Terminal window or command line. 
 Navigate to the <deepadungpalaung> directory created in subsection 1 and type the following command: <cldfbench catconfig>. This process will enable the glottolog.
 
 14. Lastly, type or paste the following command line: <cldfbench lexibank.makecldf.>. 
 This will recreate the <deepadungpalaung/cldf/forms.csv> and when you rerun the <cognate\_detection.py> and the first subsection again, it will create a different result.