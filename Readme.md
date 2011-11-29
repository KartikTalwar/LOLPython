

# LOLPython!


## WHATZ LOLPython?

Example code to generate all Fibonacci numbers less than a given value of N. Max value is 100 if N is not given on the command line. Idea derives from original lolcode implementation by Kieran O'Niell.


	IN MAI datetime GIMME date LIKE DATE

	SO IM LIKE FIBBING WIT N OK?
	    LOL ITERATE FIBONACCI TERMS LESS THAN N /LOL
	    SO GOOD N BIG LIKE EASTERBUNNY
	    BTW, FIBONACCI LIKE BUNNIES! LOL
	    U BORROW CHEEZBURGER
	    U BORROW CHEEZBURGER
	    I CAN HAZ CHEEZBURGER
	    HE CAN HAZ CHEEZBURGER
	    WHILE I CUTE?
		I AND HE CAN HAZ HE AND I ALONG WITH HE
		IZ HE BIG LIKE N?
		    KTHXBYE
		U BORROW HE

	IZ __name__ KINDA LIKE "__main__"?
	    COMPLAIN "NOW IZ" AND DATE OWN today THING
	    IZ BIGNESS ARGZ OK KINDA LIKE 1?
		N CAN HAS 100
	    NOPE?
		N CAN HAS NUMBR ARGZ LOOK AT 1!!
	    GIMME EACH I IN UR FIBBING WIT N OK?
		VISIBLE I



and in action (you must first install the most excellent [PLY](http://www.dabeaz.com/ply/) package):


	% python lolpython.py fib.lol 60
	NOW IZ 2007-06-01
	1
	1
	2
	3
	5
	8
	13
	21
	34
	55
	
	
	
It works by coverting the LOLPython code into Python. The converted Fibonacci in Python is:


	# LOLPython to Python converter version 1.0
	# Written by Andrew Dalke, who should have been working on better things.

	# sys is used for COMPLAIN and ARGZ
	import sys as _lol_sys

	from datetime import date as DATE 

	def FIBBING ( N ) :
	    'ITERATE FIBONACCI TERMS LESS THAN N' 
	    assert N >= 0 
	    # BTW, FIBONACCI LIKE BUNNIES! LOL
	    yield 1 
	    yield 1 
	    I = 1 
	    HE = 1 
	    while 1:
		I , HE = HE , I + HE 
		if HE >= N :
		    break 
		yield HE 

	if __name__ == '__main__' :
	    print >>_lol_sys.stderr, 'NOW IZ' , DATE . today ()
	    if len(_lol_sys.argv) == 1 :
		N = 100 
	    else :
		N = int(_lol_sys.argv[ 1 ]) 
	    for I in FIBBING ( N ) :
		print I 

	# The end.	
	
	

## Using LOLPython on the command line


### Run a program from stdin

	% echo "VISIBLE 'HAI WORLD!'" | python lolpython.py
	HAI WORLD!
	%	
	
	
### Translate a program from stdin into Python on stdout

	% echo "COMPLAIN 'HAI WORLD!'" | python lolpython.py --convert
	# LOLPython to Python converter version 1.0
	# Written by Andrew Dalke, who should have been working on better things.


	# sys is used for COMPLAIN and ARGZ
	import sys as _lol_sys

	print >>_lol_sys.stderr, 'HAI WORLD!' 

	# The end.


### Specify the LOLPython program filename on the command line

	% cat count_letters.lol
	LETTERZ CAN HAS INVISIBLE BUCKET
	F CAN HAS open WIT "count_letters.lol"!
	S CAN HAS F OWN read THING
	GIMME EACH C IN THE S?
	    N CAN HAS LETTERZ OWN get WIT C AND 0! ALONG WITH CHEEZBURGER
	    LETTERZ LET THE C OK CAN HAS N
	GIMME EACH C IN THE sorted WIT LETTERZ OK?
	    VISIBLE repr WIT C! AND LETTERZ LOOK AT C!
	% python lolpython.py count_letters.lol | head
	'\n' 8
	' ' 67
	'!' 4
	'"' 2
	'.' 1
	'0' 1
	'?' 2
	'A' 16
	'B' 4
	'C' 15



### Translate one or more LOLPython program files into Python files

	% python lolpython.py --convert count_letters.lol
	% cat count_letters.py 
	# LOLPython to Python converter version 1.0
	# Written by Andrew Dalke, who should have been working on better things.


	# sys is used for COMPLAIN and ARGZ
	import sys as _lol_sys

	LETTERZ = {}
	F = open ( 'count_letters.lol' ) 
	S = F . read ()
	for C in S :
	    N = LETTERZ . get ( C , 0 ) + 1 
	    LETTERZ [ C ] = N 
	for C in sorted ( LETTERZ ) :
	    print repr ( C ) , LETTERZ [ C ] 

	# The end.





