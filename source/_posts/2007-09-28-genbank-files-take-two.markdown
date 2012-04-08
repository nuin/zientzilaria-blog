---
author: admin
date: '2007-09-28 09:50:27'
layout: post
slug: genbank-files-take-two
status: publish
title: 'GenBank files: take two'
wordpress_id: '56'
? ''
: - Section 7
---

Last time we saw how to extract the sequence from our GenBank file, but
the final result might not be as nice as we wanted it to be. So, we need
to make it prettier. Running last entry's script we end up with this
sequence 

>1 gtttggtcct aaccttgtaa tcaattttta cttaatatac acatgcaagt ctccgcaccc
>61 ctgtgaaaac gcccttaaat cccccatggg ataaggagct ggtatcaggc acgaaaatct   
121 gcccaaaaca cctagctatg ccacacccac aagggtactc agcagtgattgacattattt   
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
2401 acgattaaaa ccct //


Notice that there were no mention to
the `//` at the end of the file This double slash represents the EOF of
a GenBank file. Ideally we need to remove it from the final output, as
we need to remove the nucleotide number at the beginning of each line.
In order to do that we need to modify our last script. First we will add
a condition on the `for` loop that will take care of the double slash at
the end. Then we need to use a trick to remove the numbers from the
lines. 

We should expect the numbers to be at the beginning of the line,
and never in another place. The long way would be to create a regular
expression and then replace every number occurrence with an empty
string. But Python comes with batteries included, so we will take the
short path. We use the `lstrip` string method that will remove
characters from the left part of the string, and set it to remove
numbers from 0 to 9 and the extra space before the nucleotides. And our
script will like this: 

{% codeblock lang:python %}import sys 
gbfile = open(sys.argv[1], 'r').readlines() 
sequence = '' issequence = False 
for line in gbfile: 
	if issequence == True and not line.find('/') == 0:
		sequence += line.lstrip('0123456789 ') 
	elif line.find('ORIGIN') >= 0:
		issequence = True 
		print sequence{% endcodeblock %} 
		
		
Notice that the first `if`
condition was modified to include a condition that we do **not** find a
slash. And at the line where we concatenate the sequence we added a
`lstrip('0123456789 ')` to modify the string on the fly. The final
result looks much better now. But we still have a small "problem": there
are spaces between groups of 10 nucleotides and we want to get rid of
them. We would be surprised if it was difficult, and as expected it is
not. We used [here](http://python.genedrift.org/2007/09/07/restrinction-enzymes-second-take/)
the replace method and we can use it here too. We only need to modify
the line that concatenates the sequence, and our final script will be


{% codeblock lang:python %}import sys 
gbfile = open(sys.argv[1], 'r').readlines() 
sequence = '' 
issequence = False 
for line in gbfile:
	if issequence == True and not line.find('/') == 0: 
		sequence += line.lstrip('0123456789 ').replace(' ', '') 
	elif line.find('ORIGIN') >= 0: 
		issequence = True 
		print sequence{% endcodeblock %} 


Notice that we add the
`replace` method after the `lstrip`, but it can either way. The output
should be only the nucleotides, with no space or numbers.
