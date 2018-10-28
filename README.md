# hangman
# Hangman code I got that is hardcoded and needs reviewed to work. oh I'm a newbie trying to learn it's hard coded and I am trying to learn how to un hard code it.
import random

board = ['''

>>>>>>>>>>Hangman<<<<<<<<<<

+---+
|   |
    |
    |
    |
    |
=========''', '''

+---+
|   |
O   |
    |
    |
    |
=========''', '''

+---+
|   |
O   |
|   |
    |
    |
=========''', '''

 +---+
 |   |
 O   |
/|   |
     |
     |
=========''', '''

 +---+
 |   |
 O   |
/|\  |
     |
     |
=========''', '''

 +---+
 |   |
 O   |
/|\  |
/    |
     |
=========''', '''

 +---+
 |   |
 O   |
/|\  |
/ \  |
     |
=========''']


class Hangman:
	def __init__(self,word):
		self.word = word
		self.missed_letters = []
		self.guessed_letters = []
		
	def guess(self,letter):
		if letter in self.word and letter not in self.guessed_letters:
			self.guessed_letters.append(letter)
		elif letter not in self.word and letter not in self.missed_letters:
			self.missed_letters.append(letter)
		else:
			return False
		return True
		
	def hangman_over(self):
		return self.hangman_won() or (len(self.missed_letters) == 6)
		
	def hangman_won(self):
		if '_' not in self.hide_word():
			return True
		return False
		
	def hide_word(self):
		rtn = ''
		for letter in self.word:
			if letter not in self.guessed_letters:
				rtn += '_'
			else:
				rtn += letter
		return rtn
		
	def print_game_status(self):
		print (board[len(self.missed_letters)])
		print ('Word: ' + self.hide_word())
		print ('Letters Missed: ',) 
		for letter in self.missed_letters:
			print (letter,) 
		print ()
		print ('Letters Guessed: ',)
		for letter in self.guessed_letters:
			print (letter,)
		print ()

def rand_word():
        with open("/home/pi/Downloads/words.txt", "rt") as f:
                bank=f.readlines()
        return bank[random.randint(0,len(bank))]

def main():
	game = Hangman(rand_word())
	while not game.hangman_over():
		game.print_game_status()
		user_input = input('\nEnter a letter: ')
		game.guess(user_input)

	game.print_game_status()	
	if game.hangman_won():
		print ('\nCongratulations! You have won!!')
	else:
		print ('\nSorry, you have lost.')
		print ('The word was ' + game.word)
		
	print ('\nGoodbye!\n')
		
if __name__ == "__main__":
	main()
