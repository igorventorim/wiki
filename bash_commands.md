1 - The "last argument" one: !$

2 - The "nth argument" on: !:2

	$ tar -cvf afolder afolder.tar
	tar: failed to open

	$ !:0 !:1 !:3 !:2
	tar -cvf afolder.tar afolder

3 - The "all the arguments" one: !:1-$

	$ grep '(ping|pong)' afile
	$ egrep !:1-$
	egrep '(ping|pong)' afile
	You don't need to pick 1-$; you can pick a subset like 1-2 or 3-9;

4 - The "last but n" one: !-2:$
	$ mv /path/to/rightfile !-2:$

5 - The "get me the folder" one: !$:h
	$ tar -cvf system.tar /etc/system
	tar: /etc/system: Cannot stat: No such file or directory
	$ cd !$:h
	cd /etc

6 - The "the current line" one: !#:1
	$ cp /path/to/some/file !#:1.bak 
	cp /path/to/some/file /path/to/some/file.bak

7. The "search and replace" one: !!:gs

	Say I want to tell the world that my s key does not work and outputs f instead:
	$ echo my f key doef not work
	$ !!:gs/f /s /
	echo my s key does not work
	
