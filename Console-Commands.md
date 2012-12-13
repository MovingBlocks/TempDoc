This is an article for developers who want to use and create their own console commands (for example for mods).

Adding new console commands to Terasology is easy. The steps below show what is needed for console commands.
Command implementation

Command structure
==============

Every command must be implemented as a public method. E.g. the following command just displays "hello world" in the console.

<pre>
    public class MyCommands implements CommandProvider {

        @Command( shortDescription = "Say hello", helpText = "Writes hello world to the console" )
        public void hello() {
            MessageManager.getInstance().addMessage("hello world");
        }

    }
</pre>

Looking at this simple examples we can see several important things:
* The command method must be located in a class implementing ``CommandProvider``
* The command annotation ``@Command`` is necessary for every command
* One can specify a short description and a (probably) longer help text
* The console can be accessed via the ``MessageManager``

Creating own console commands
------------------
If you want to create a new console command, you must use one of the existing ``CommandProvider`` classes (such as
the ``Commands`` class) or create a new class implementing the interface.

To specify a new console command, just an annotated public method is needed. The annotation is
<pre>
    @Command()
</pre>
and marks the method as a command. The command will have the same name as the method,
e.g. if you name you method ``public void hello`` the command ``/hello`` will be available in the game.

Short Descriptions and Help Text
-----------------
Short descriptions and help texts can be added via the method annotation. To specify a short description, just add
<pre>
    shortDescription = "text for short description"
</pre>
to the annotation, e.g.
<pre>
    @Command( shortDescription = "some command description" )
</pre>

Probably longer help text can be specified via ``helpText`` in the annotaion. An example is given below:
<pre>
    @Command( helpText = "A command without short description, but with a longer help text." )
</pre>


Displaying text
------------------
To display text in the in game console, you have to use ``MessageManager`` class. Simple console output can be
achieved via
<pre>
    MessageManager.getInstance().addMessage("Text to display")
</pre>

Parameters
-------------------
Of course it is possible to give parameters/arguments to your command when executed in the command line. These
arguments are specified as method arguments. It is highly recommended to prefix the method arguments by a parameter
annotation, that is used for the command line help.
<pre>
    @Command( shortDescription = "Echo-cho-cho-o-o", helpText = "Echoes the input text." )
    public void echo(@CommandParam( name = "Message" ) String message){
        MessageManager.getInstance().addMessage(message);
    }
</pre>
The method above will add an ``/echo`` command that simply echoes the input text. The command is proper annotated,
resulting in user friendly help messages and command description.

Commands class
-------------

The Commands class should contain all core commands. Such are commands related to blocks and items.
