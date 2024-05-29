all: concat_files

concat_files: my_file1 my_file2
	cat my_file1 > concat_files
	echo >> concat_files
	cat my_file2 >> concat_files

my_file1:
	echo "File 1" > my_file1

my_file2: content.txt
	echo 'Here is some content from content.txt:' > my_file2
	cat content.txt >> my_file2
