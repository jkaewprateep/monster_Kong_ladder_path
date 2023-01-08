# monster_Kong_ladder_path ( Pending waits game creators action )

For create environment for AI study (pending from the game action ladder)

```
"""""""""""""""""""""""""""""""""""""""""""""""""""""""""
: Class / Functions
"""""""""""""""""""""""""""""""""""""""""""""""""""""""""
def	read_current_state( string_gamestate ):
		
	if string_gamestate in ['score']:
		return game_console.getScore()
		
	elif string_gamestate in ['game_over']:	# False
		return game_console.game_over()
		
	elif string_gamestate in ['fireballGroup']:
		temp = []
		for fireball in game_console.newGame.fireballGroup :
			temp.append( fireball.getPosition() )	
		return temp
		
	elif string_gamestate in ['coinGroup']:
		temp = []
		for coin in game_console.newGame.coinGroup :
			temp.append( coin.getPosition() )	
		return temp
		
	elif string_gamestate in ['player']:
		Player_Game = game_console.newGame.Players
		( width, height ) = p.getScreenDims()
		temp = []
		for player in game_console.newGame.Players :
		
			# None, Left, Down, Right, Up, Action
			# player = ( 	1, 1, 1, 
						# 1, 1, 1,
						# 1, 1, 1
					   # )
		
		
			x = player.getPosition()[0]
			y = height - player.getPosition()[1]
			# temp.append( [( x - 2.5, y + 2.5 ),( x, y + 2.5 ),( x + 2.5, y + 2.5 ),( x - 2.5, y ),( x , y ),
      ( x + 2.5, y ),
      ( x - 2.5, y - 2.5 ),( x, y - 2.5 ),( x + 2.5, y - 2.5 )] )	
			temp.append( ( x, y ) )
		return temp
		
	elif string_gamestate in ['monster']:
		MonsterPerson_Game = game_console.newGame.Enemies
		temp = []
		for Enemies in MonsterPerson_Game :
			temp.append( Enemies.getPosition() )	
		return temp
		
	elif string_gamestate in ['lives']:
		return game_console.newGame.lives
		
	elif string_gamestate in ['allies']:
		Allies_Game = game_console.newGame.allyGroup
		temp = []
		for allies in Allies_Game :
			temp.append( allies.getPosition() )	
		return temp
		
	elif string_gamestate in ['wall']:
		Wall_Game = game_console.newGame.wallGroup
		temp = []
		for wall in Wall_Game :
			temp.append( wall.getPosition() )	
		return temp
		
	elif string_gamestate in ['ladder']:
		Ladder_Game = game_console.newGame.ladderGroup
		( width, height ) = p.getScreenDims()
		temp = []
		for ladder in Ladder_Game :
			x = ladder.getPosition()[0]
			y = height - ladder.getPosition()[1] + 1.0
			
			### ladder width 15 pixels ###
			# ladder ===> player: (215.0, 58.5) ===> player: (200.0, 58.5)
			# In ladder list ===> (205.0, 58.5)
			# x_target = x + 7.5
			# y_target = y
			temp.append( ( x, y, x - 2.5, y - 2.5, x + 7.5, y + 12.0 ) )	
		return temp
		
	elif string_gamestate in ['map']:
		Map_Game = game_console.newGame.map	# 30x80
		return Map_Game	
		
	else:
		return None
		
	return None

def action_perform( action ):
	reward = p.act(list(actions.values())[action])
	
	player = read_current_state('player')[0]
	has_ladder = [ ( a, b, c, d, e, f ) for ( a, b, c, d, e, f ) in ladders if player[0] >= c and 
                  player[0] <= e and player[1] >= d and player[1] <= f ]
	print( "Has Ladder: " + str(bool(len(has_ladder))) )
	
	return

def random_action_perform( ): 
	
	temp = tf.random.normal([1, 6], 0.1, 0.1, tf.float32)
	temp = tf.math.multiply(temp, tf.constant([ 0.0000099, 99999999, 0.0000099, 
                          99999999, 0.0000099, 99999999 ], shape=(6, 1), dtype=tf.float32))
	action = int(tf.math.argmax(temp[0]))

	return action
```

![Try ladder escape](https://github.com/jkaewprateep/monster_Kong_ladder_path/blob/main/monster_kong.gif "Try ladder escapes")



