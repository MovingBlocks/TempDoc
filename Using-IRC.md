%META:TOPICINFO{author="RasmusPraestholm" comment="save topic" date="1328571884" format="1.1" reprev="2" version="3"}%
%META:TOPICPARENT{name="WebHome"}%
---+!! Setting up IRC

%TOC%

It can be a little awkward getting set up for IRC fully if you don't want to just use the quick web chat option at http://webchat.freenode.net

---++ User setup

For plain user signups and general info

   * Pick a client - loads of these available, even as browser plugins for Firefox and Chrome
   * Connect to irc.freenode.net - see http://freenode.net/using_the_network.shtml for more details
   * IRC generally dumps you in a system channel and expects you to use slash commands or menus to get stuff done 
      * Make sure any options in your client are set with your right name, nick, desired starting channel (#terasology), etc
      * You can set / change your nick by simply entering =/nick [mynick]=
      * If you want to safeguard your nickname / account register it by entering: =/msg nickserv register [pass] [email]= (while you're online with your preferred nick)
      * This will send you an email with a verification command to enter to verify your account
      * To then re-identify yourself to the server on each login you may have to enter a command like =/msg nickserv identify [pass]= - most clients will allow you to automatically issue that on startup
   * For additional help enter =/msg nickserv help=
   * Note that typical IRC usage involves people leaving their computers online and in channel without actually checking constantly, just catching up once in a while. Be patient - there is no intent to ignore you :-) 
      * Still, forum is better for guaranteed response if needed - after all, computers lose connectivity or even power from time to time

---++ Gooey

Our friendly local IRC bot. Lives at https://github.com/MovingBlocks/Gooey and is based on hubot - more details TODO

---++ Admin stuff

More advanced stuff casual users shouldn't need

   * Add operator status automatically to core team (done by the !ChanServ bot): =/msg !ChanServ FLAGS #terasology [nick] +votriA=
      * Which then may fall off if you relog, in that case just ask !ChanServ to share its omnipotence by entering: =/msg !ChanServ OP #terasology [nick]=
   * Log out if you need to register a separate account (like for a robot): =/ns logout= (then change nick and do the nickserv register thing - you'll then have to do the identify thing for yourself again)

---++ Helpful links

   * Tutorial & terms: http://www.irchelp.org/irchelp/irctutorial.html
