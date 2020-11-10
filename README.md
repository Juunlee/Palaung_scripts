Tutorial 

(1)Cloning and installing the repositories 
 1. Readers should make sure to have Python 3 and git installed on the computer.
  If so, open a git-enabled Terminal window or command line.
  
 2. Even though it is not required, we strongly recommend the readers create a new Python virtual environment for the following process, as a few packages will be installed. 
 A new Python virtual environment can be created anywhere and the commands to create it in the current folder and launch it are:
 <python -m venv .> or <python3 -m venv .> followed by <source bin/activate> on Mac or Linux,
 <Scripts\ activate> on a standard Windows command line, or <source Scripts/activate> on Windows using git bash.
 More information can be found at <https://docs.python.org/3/library/venv.html>.
 
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
 If the terminal instead outputs an error related to <igraph>, simply run <pip uninstall igraph> followed by <pip install python-igraph> to fix this error.
 
 8. This distance matrix created by the program can be turned into a tree by using two methods. 
 First, readers can open the csv in a text editor and paste it as text into DendroUPGMA at <http://genomes.urv.cat/UPGMA/> choosing option (c) a distance matrix. 
 This decorates an internal node with the distance to any of its leaves, and was the method used to generate the images in this paper.
 
 9. The second method is by using the <UPGMA.p> in the <Palaung\_scripts/> directory.
 In the terminal, type the following command: <python UPGMA.py>. Then, type the same method that was used to create the distance matrix.
 The UPGMA script will then run, outputting the number of nodes left to work on as it goes.
  
 10. This method will create a file in <deepadungpalaung/output/> called <tree\_lexstatcogids.xml> (in the case of lexstatcogids), which
 can then be opened in a web browser to see internal nodes decorated with the average distance between the two groups joined. 
 Note that this number would be greater than the number given by the tree display in step 8.
 
(3)Editing orthography.tsv and remaking the CLDF

 11. Type or paste the following command lines: <cldfbench catconfig> and <cldfbench lexibank.makecldf deepadungpalaung>
 This will recreate the file <cldf/forms.csv> in <deepadungpalaung> according to the transcription rules written at <etc/orthography.tsv>. 
 One should see no difference between the new <forms.csv> and the old one.
 <Wu et al., 2020 > tells you how to view the file <forms.csv> in EDICTOR.

 12. By editing the <orthography.tsv>, one can change which standard phonetic symbol should be used to represent various nonstandard phonetic symbols used by linguists in the raw data <Anderson et al., 2018> <Forkel and List, 2020>. 
 One can also divide words into different numbers of morphemes, or split the words into morphemes in different places.
 In order to open <orthography.tsv> for editing, one can use either text editors such as Notepad, Notepad++, TextEdit, and BBEdit, or a spreadsheet editor such as OpenOffice and LibreOffice.
 In the first column of <orthography.tsv>, users input the graphemes that will be changed. Then, in the second column (or, in a text editor, by pressing Tab), users can write down the change they want to make for that sequence.
 
 13. For example, if the user inputs <tʃ> in the first column and writes down <t ʃ> in the second column, this sequence of two graphemes will be considered separate segments <t> and <ʃ> in <deepadungpalaung/cldf/forms.csv>.
 If, on the other hand, the user inputs <tʃ> in the first column and writes down <tʃ> in the second column, this sequence of two graphemes will be considered a single segment, the affricate.
 If the user writes <tʃ> in the first column and writes down <t + ʃ>, this sequence of two graphemes will be considered to always contain a syllable boundary.
 
 14.  The user can also indicate that a word-beginning or word-ending context should affect the transformation, using ^ and $, respectively. Consider the chart in the tutorial of the paper.
 <t> and <ʃ> will be considered separate segments unless <tʃ> appears in the beginning of the word or at the end of the word. However if the word is either <tʃat> or <tʃatarem>, the two graphemes will still be considered separate segments. 
 In addition, it will separate the word <tʃatarem> into three morphemes as well, which can then be compared to morphemes in words of other languages when the script is run and a partial cognate method is chosen.
 
 15. In <orthography.tsv>, there are a lot of characters that look the same but have different unicode codepoints. For instance, in line 220 and 245, both instances of <ʔ> look similar but they have different unicodes; one is a Latin capital letter glottal stop and the other is Latin letter glottal stop. 
 If a user's changes to <orthography.tsv> have caused Unicode symbols that are not accepted phonetic symbols to remain in <cldf/forms.csv> after running <cldfbench lexibank.makecldf>, these errors will be recorded at <TRANSCRIPTION.md> in <deepadungpalaun>. Users can browse to <http://unicode.scarfboy.com/><Unicode lookup> and paste characters from <TRANSCRIPTION.md> in to make sure that they are writing the correct character in the left column of <orthography.tsv>.
 
 16. After editing the <orthography.tsv>, open a git-enabled Terminal window or command line.
 Type the following command: <cldfbench catconfig>
 This process will enable the Glottolog.
 
 17. Lastly, type or paste the following command line: <cldfbench lexibank.makecldf>
 This will recreate the file <cldf/forms.csv> in <deepadungpalaung/> and when you rerun <cognate\_detection.py> and steps 6-10 again, it will create a different result.
 
 (4)Adapting the script to other Lexibank datasets
 18. The script can also be used to analyze any of several other datasets from Lexibank. To find such a dataset, browse <https://github.com/lexibank/><github.com/lexibank/> and change the first line of <Palaung\_scripts/cognate\_detection.py}> from <from lexibank\_deepadungpalaung import Dataset>  to e.g. <from lexibank\_chindialectsurvey import Dataset>.
 Now if users have also followed steps 3 and 4 with <deepadungpalaung> replaced by e.g. <chindialectsurvey>, it will construct a phylogenetic tree of Chin dialects.