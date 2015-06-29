# BULC2015
Python Code
def alignment(string1, string2):
	i, j = 0, 0
	string1 = '_' + string1
	string2 = '_' + string2
	def score(i, j): #are the two characters the same?
		if i < len(string1) and j < len(string2):
			if string1[i] == string2[j]:
				return 0
			else: 
				return 1
	def M(i, j, grid): #determines the score of a particular box
		if i != 0 and j != 0: #rest of matrix
			return min(grid[j-1][i] + 1, grid[j][i-1] + 1, grid[j-1][i-1] + score(i, j) )
		elif i == 0 and j == 0:#origin
			return 0
		else:#first row/ column
			if i == 0:
				return grid[j-1][i] + 1
			elif j == 0:
				return grid[j][i-1]+ 1
	matrix = []
	for uneeded in range(0, len(string2)):
		matrix.append([])
	for j in range(0, len(string2)):
		for i in range(0, len(string1)):
			matrix[j].append(M(i,j,matrix))
		print matrix[j]
	sequence1, sequence2 = '', ''
	i, j = len(string1) - 1, len(string2) - 1
	while i > 0 and j > 0: #go through matrix and add letters
		if matrix[j][i] == matrix[j-1][i-1] + score(i, j): #diagonal
			sequence1 = sequence1 + string1[i]
			sequence2 = sequence2 + string2[j]
			i = i - 1
			j = j - 1
		elif matrix[j][i] == matrix[j][i-1] + 1: #horizontal
			sequence1 = sequence1 + string1[i]
			sequence2 = sequence2 + '-'
			i = i - 1
		elif matrix[j][i] == matrix[j-1][i] + 1: #vertical
			sequence1 = sequence1 + '-'
			sequence2 = sequence2 + string2[j]
			j = j - 1
	if i == 0 and j != 0:
		while j > 0:
			sequence2 = sequence2 + string2[j]
			sequence1 = sequence1 + '-'
			j = j - 1
	elif j == 0 and i != 0:
		while i > 0:
			sequence2 = sequence2 + '-'
			sequence1 = sequence1 + string1[i]
			i = i - 1
	sequence1 = sequence1[::-1]
	sequence2 = sequence2[::-1]
	# above two lines reverse string order
	print sequence1
	print sequence2
	return
