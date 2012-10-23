---
author: Paulo Nuin
date: '2007-09-27 16:13:14'
layout: post
slug: genbank-files
status: publish
title: 'GenBank files: take one'
wordpress_id: '55'
? ''
: - Section 7
---

We are back, moving to a new chapter of the book and starting a new
section on the site. This chapter deals with the manipulation of
[GenBank](http://www.ncbi.nlm.nih.gov) files. These files are used by
NCBI to store information about RNA, DNA and protein sequences. It is
usually composed of an annotation section, that gives information about
the sequence present in the particular file. I won't spend much time
explaining the GenBank format, because it is not the goal of the site.
The perl book has some good explanation about it and you can also find
more information
[here](http://www.umanitoba.ca/afs/plant_science/psgendb/doc/GenBank/gbrel.txt).
Also, we are going to see here some of the characteristics of such
files. The GenBank file we are going to manipulate from now on is this
one

`LOCUS       DQ283072                2414 bp    DNA     linear   VRT 12-MAR-2010
DEFINITION  Megaelosia goeldii voucher Paulo Nuin 12S ribosomal RNA gene,
            partial sequence; tRNA-Val gene, complete sequence; and 16S
            ribosomal RNA gene, partial sequence; mitochondrial.
ACCESSION   DQ283072
VERSION     DQ283072.1  GI:90296241
KEYWORDS    .
SOURCE      mitochondrion Megaelosia goeldii (Rio big-tooth frog)
  ORGANISM  Megaelosia goeldii
            Eukaryota; Metazoa; Chordata; Craniata; Vertebrata; Euteleostomi;
            Amphibia; Batrachia; Anura; Neobatrachia; Hyloidea; Hylodidae;
            Megaelosia.
REFERENCE   1  (bases 1 to 2414)
  AUTHORS   Frost,D.R., Grant,T., Faivovich,J., Bain,R., Haas,A.,
            Haddad,C.F.B., de Sa,R.O., Channing,A., Wilkinson,M.,
            Donnellan,S.C., Raxworthy,C., Campbell,J.A., Blotto,B.L., Moler,P.,
            Drewes,R.C., Nussbaum,R.A., Lynch,J.D., Green,D.M. and Wheeler,W.C.
  TITLE     The Amphibian Tree of Life
  JOURNAL   Bull. Am. Mus. Nat. Hist. 297, 1-291 (2006)
REFERENCE   2  (bases 1 to 2414)
  AUTHORS   Frost,D.R., Grant,T., Faivovich,J., Bain,R., Haas,A.,
            Haddad,C.F.B., de Sa,R.O., Channing,A., Wilkinson,M.,
            Donnellan,S.C., Raxworthy,C., Campbell,J.A., Blotto,B.L., Moler,P.,
            Drewes,R.C., Nussbaum,R.A., Lynch,J.D., Green,D.M. and Wheeler,W.C.
  TITLE     Direct Submission
  JOURNAL   Submitted (26-OCT-2005) Herpetology, Division of Vertebrate
            Zoology, American Museum of Natural History, Central Park West at
            79th Street, New York, NY 10024, USA
FEATURES             Location/Qualifiers
     source          1..2414
                     /organism="Megaelosia goeldii"
                     /organelle="mitochondrion"
                     /mol_type="genomic DNA"
                     /specimen_voucher="Paulo Nuin"
                     /db_xref="taxon:209670"
                     /country="Brazil: Rio de Janeiro, Teresopolis, Rio Beija
                     Flor, 910 m, 22'24'S, 42'69'W"
     misc_feature    <1..>2414
                     /note="contains 12S ribosomal RNA, tRNA-Val, and 16S
                     ribosomal RNA"
ORIGIN      
        1 gtttggtcct aaccttgtaa tcaattttta cttaatatac acatgcaagt ctccgcaccc
       61 ctgtgaaaac gcccttaaat cccccatggg ataaggagct ggtatcaggc acgaaaatct
      121 gcccaaaaca cctagctatg ccacacccac aagggtactc agcagtgatt gacattattt
      181 ataagcgcca gcttgactca gttaaagtaa agagagccgg caaatctggt gccagccgcc
      241 gcggttaccc cacgtggctc aaattgattt ctttcggcgt aaagcgtgat taaagtgccc
      301 atcaacattg gagttaaact aaaattaagc tgtgacacgc ttattttaca gaaaagcaca
      361 aacgaaagtt acttcaattt aaacaacttg aattcacgac agtcaggaca caaactggga
      421 ttagataccc cactatgccc gaccgtaaac tttaatttac accatcaccg ccagagaact
      481 acgagcaaag cttaaaactc aaaggacttg acggtccccc acatccccct agaggagcct
      541 gtcctttaat cgataatccc cgcttaacct caccattctt agtctttcag cctgtatacc
      601 tccgtcgtca gcttaccccg tgagcgaaaa ttagtgagct taatgtccac acgtctacac
      661 gtcaggtcaa ggtgcagcaa atataatggg aagagatggg ctacactttc tagtctagaa
      721 tatacgaaag accacctatg aaacctggtc agaaggcgga tttagaagta aaaggaaacc
      781 agagcatccc ttttaatttg gcactggggc atgtacacac cgcccgtcac cctcttcaaa
      841 gcctaatttt agtatctaac caactaacgc ctagtagaag aggcaagtcg taacatggta
      901 agtataccgg aaggtgtgct tggaaacaaa atatagccta atcaaagcat ttcgcttaca
      961 ccgaaaagtt atctgtgaaa ttcagattat tttgagctaa aaatctagcc ccactttatt
     1021 ctataatccc ttatcactta aattcatgaa tcaaaacatt ttaataatca agtaaaggcg
     1081 attgaaaaat taataggagc aatatatact gtaccgcaag ggaaagatga aatagaaatg
     1141 aaataataat taaagcataa aaaagtaaag attaaatctt gtaccttttg catcatgatt
     1201 taactagtct acccaggcaa aatgatttta agtctgacct cccgaaacta agtgagctac
     1261 ttcaaggcag cttaatgagc aaatccgtct ctgtcgcaaa agagtggaga gaccttcaag
     1321 tagaagtgat agacctaacg aacttagtaa tagctggtta ttcaagaaaa ggatctcagt
     1381 ccaacctaaa gtcaaattaa tgtttaaaaa taaaaattct gaccttagag taattcaatt
     1441 aaggtacagc ctacttgaaa caggatacaa ccttaactaa tgggtaactt accccttcat
     1501 cttttaagtg ggcctaaaag cagccacctt taaaatagcg tcaaagctta gccgtcctat
     1561 acatctaata ccaaaaacat ctatgaaccc tatactcata ttgaataatt ctatattatt
     1621 atagagattt ttatgttaaa actagtaaca agaattaaat tttctctatt atgttcgtgt
     1681 acatcagaaa ggataaacca ctgataattg acatgcatga gtaaaaagca gtaacttaac
     1741 aagaaaaccc tcctaactct aatgttaacc taacacaagt acatctcaag aaagatttaa
     1801 agaaaaagaa ggaactcggc aaacattaac ctcgcctgtt taccaaaaac atcgcctctt
     1861 gtcaaaattt aagaggtcca gcctgcccag tgaccctgtt caacggccgc ggtatcctaa
     1921 ccgtgcgaag gtagcgtaat cacttgttct ttaaataagg actagtatga atggcaccac
     1981 gagggttata ctgtctcctt tttctaatca gtgaaactaa tcttcccgtg aagaagcggg
     2041 aatttttata taagacgaga agaccctatg gagctttaga cgagtaacaa ctgctaattt
     2101 tataatattt cagataatat ctctatccta gcattatgat tataagtctt tggttggggt
     2161 gaccgcggag aaaaaaataa cctccacatt gaaagaatat tattctaagc aaaaagacac
     2221 atctttaagc atcaacaaat tgacatctat tgacccaata ttttgatcaa cgaaccaagt
     2281 taccctaggg ataacagcgc aatccacttc gagagctctt atcgacaagt gggcttacga
     2341 cctcgatgtt ggatcagggt atcctagtgg tgtagccgct actaaaggtt cgtttgttca
     2401 acgattaaaa ccct
//`

which stores a sequence of a mitochondrial gene of a stream frog from
South America, called *Megaelosia goeldii*, also known as Rio big-tooth
frog. (get a better formatted file [here](http://python.genedrift.org/megaelosia.gbk)) Our fast task will
be to extract the DNA sequence from the file. This sounds easy, and not
surprisingly it is. If we take a closer look at the file we will see
that the sequence starts after the mark **ORIGIN**. From what we have
seen before we just need to read the file, the a boolean variable that
checks for **ORIGIN** and concatenate everything after that. Something
like this 

{% codeblock lang:python %}import sys
 
gbfile = open(sys.argv[1], 'r').readlines()
 
sequence = ''
issequence = False
for line in gbfile:
    if issequence == True:
        sequence += line
    elif line.find('ORIGIN') >= 0:
        issequence = True
 
print sequence
		{% endcodeblock %}


Quick and easy. When we find **ORIGIN**, `issequence` has its state
changed to True and the lines below will concatenated into a string. We
print at the end. Next time we will do more fancy things.
