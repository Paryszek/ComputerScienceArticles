# Command Pattern

Did you ever struggled with maintaining several independent behaviors inside single class? The Command Pattern comes with rescue. The pattern is very easy, it helps to organize the code and improves readability. It’s good tool for every software engineer to hold on for the future coding sessions. 

As example, I used some typical player from the typical game which is controlled by user inputs, but I am sure it can be just as good in other circumstances - even outside game development.

Below is shown typical way of implementing separate player behaviors.

```csharp
public class Player {
	private Controls controls;

	GameLoop() {
		handleInput();
	}

	HandleInput() {
		if(controls.leftArrow) moveLeft();
		if(controls.rightArrow) moveRight();
		if(controls.spacebar) jump();
		if(controls.shift) slide();
	}

	// ... moveLeft(), moveRight(), jump(), slide() methods
}
```

This implementation is not that bad, it works and can be good for first code base of Player class. The problems can appear in the future when there will be need to expand the class. Command Pattern is a good way to clean up the player input methods.

As I said the pattern is fairly easy, for every behavior we create separate class that implements abstract CommandBase class with Execute method. 

```csharp
public abstract class CommandBase {
	abstract void Execute();
}

public class JumpCommand: CommandBase {
	private player;
	
	Command(Player player) {
		this.player = player;
	}

	public void Execute() {
		// Jump control
	}
}

class SlideCommand: CommandBase {
	...
}

class MoveLeftCommand: CommandBase {
	...
}

class MoveRightCommand: CommandBase {
	...
}
```

We extracted each behavior implementation from Player class, so now we can see how Command Pattern can bring more clarity into implementing each player control behavior. There is no need for Player class to store control methods anymore. 

It’s time to refactor our Player class with new Commands for each input.

```csharp
public class Player {
	private Controls controls;
	private JumpCommand jumpCommand;
	private MoveRightCommand moveRightCommand;	
	private MoveLeftCommand moveLeftCommand;
	private SlideCommand slideCommand;

	Init() {
		jumpCommand = new JumpCommand(this);
		moveRight = new MoveRight(this);
		moveLeft = new MoveLeft(this);
		slideCommand = new SlideCommand(this);
	}

	GameLoop() {
		handleInput();
	}

	HandleInput() {
		if(controls.leftArrow) UseCommand(moveLeft);
		if(controls.rightArrow) UseCommand(moveRight);
		if(controls.spacebar) UseCommand(jumpCommand);
		if(controls.shift) UseCommand(slideCommand);
	}

	HandleCommand(CommandBase command) {
		command.Execute();
	}
}
```

All commands are created during the Init method execution and stored in separate variables. It’s good way to prevent creating new classes for every user input occurrence, which can hurt optimization. 

Doesn’t it look amazing? Simplicity at its finest, code for player controls inside Player class is reduced to minimum. Pattern is good representation of Object Oriented Programming capabilities. Pattern gives readability together with manageability, so now its actually really easy to add new behaviors without littering the Player class.

Well, that would be all from my side, not much more to add regarding this pattern. I hope you will notice the benefits of this pattern and you will find good use for it.