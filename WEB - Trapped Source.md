Challenge name: Trapped Source

Category: WEB

Description: Intergalactic Ministry of Spies tested Pandora's movement and intelligence abilities. She found herself locked in a room with no apparent means of escape. Her task was to unlock the door and make her way out. Can you help her in opening the door?

My first-thoughts: This is a very easy challenge.... let's finish this up fast
Challenge overview: We are provided with a docker to spawn (no source code) and as soon as you spawn the docker you get some vault locker kind of webpage. All we have to do is unlock this locker.... But how do we do it?

Solution: So I saw the keypad and thought I can try entering random lock passwords like 1234, 6789, etc. None of those worked then I opened up the webpage in f12-dev menu where I was able to see all of the source code. And there I Found some javascript code in the <script> tag which looked something like this.
```
		window.CONFIG = window.CONFIG || {
			buildNumber: "v20190816",
			debug: false,
			modelName: "Valencia",
			correctPin: "8291",
		}

  Now there you have the correct pin... enter the pin "8291" and get the flag. Yea the flag is displayed when you enter 8291 in the keypad.
