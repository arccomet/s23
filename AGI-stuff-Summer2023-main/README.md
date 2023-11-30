## Devlog:
### Old topic: ~~Experiemental Multi-modal Agent (Emma) of 2023~~
### ~~This project is created in June 2023. My goal is to utilize the best open-source models currently available to create a general-purpose agent. This is meant to be an experiment for understanding what is currently possible and taking a peek into the future.~~
#### Phase one - Exploring my options
Features to include:
- Audio >> Speech Recognition, Diarization
- Visual >> Visual Question Answering, Possibly video understanding
- Think >> By using CoT or ToT, with additional prompt modification, the agent will be capable of thinking before acting.
- Memory >> Langchain, and possibly using a vector database like Pinecone. This will 
- Generative Capability >> Utilize Tools such as Stable Diffusion, or MusicGen, This will be imp

LLM:
- Wizard Vicuna Uncensored >> Valid 
- WizardLM Uncensored >> Better than Wizard Vicuna
- TheBloke/Nous-Hermes-13B-GPTQ >> great model, finetuned on gpt4
- TheBloke_guanaco-7B-GPTQ >> hallucinate a lot, but pretty good
- TheBloke_guanaco-33B-GPTQ >> 33B version is much more flexible and intelligent. This will be my go-to pick and I will have to use QLoRa to finetune this.

TTS:
- SpeechT5 is okay but not great
- Eleven Labs has no alternatives right now
- Tortoise is too slow
- Tacotron2 is old and I don’t like it.
- Bark is unstable and quite slow
- So far I can't find one that I like, so I guess I will wait for an open source TTS that rivals ElevenLabs to come. Implement later.
- 
VQA:
- Salesforce/blip-vqa-capfilt-large >> Short VQA
- Salesforce/blip-vqa-base >> Short VQA
- google/pix2struct >> a bunch of pretty interesting models for mostly UI side of captioning and vqa

Image Captioning:
- Salesforce/blip-image-captioning-large >> Pretty good model, I like it
- google/pix2struct-textcaps-base >> Good at recognizing text

Object detection:
- owlvit >> I don't like it, you need to suggest things for it to look for
- convnext >> just classification, no coordinate
- yolos >> seems pretty good, a bit too simple but I can finetune it

Voice Input:
- whisper-diarization >> implement later

#### Phase Two - Experimentation
In the spirit of trying to create some sort of self-awareness, I tried to prompt the LLM to write in first-person perspective, focusing on thoughts. I could then send the monologue to an Instruct model to extract actions for output. I still haven't figured out how to do it right, but this idea does bring a lot of possibilities.\
Also, I think the unconscious part of our brain can not be prompted, perhaps it has to be trained?

#### Phase Three - Pivot
My original plan was to create an AI that can see, hear and ask itself questions. But after looking at some Vision-capable Multimodal LLMs such as MiniGPT4, I had to face the fact that I set out to do an impossible mission. I also don't think that I should be trying to recreate what has already been done by LangChain or AutoGPT. In the end, I felt lost as everything seems to either have already been done or is not yet possible for me to do. So I took a few days off and prepared myself for the summer exams. And that brings us to June 22nd, a seemingly unproductive day, bought groceries, sat in front of my laptop, and struggled to think of anything that I can actually do, a project that is truly unique and exciting. All I got were big and unrealistic ideas such as making an LLM-powered low-poly style city simulation in Unity, or a 3D avatar with facial expressions for AI, using VRoid Studio to create the base model, which I'm not familiar with. In the end, after a day of experimenting and proving that all my ideas are stupid, I finally give up and decided to go to bed. The idea of finetuning an LLM with my custom dataset and the idea behind the LIMA paper lingered in my mind as I fall asleep.
The next day, I woke up and decided to finetune an LLM to tell less boring jokes. First I created a simple dataset with 100 jokes that I found online, put them into a dataset, and trained a LoRa model using QLoRA on LLaMa7B. The initial result isn't exactly promising, but it was a proof of concept. The next thing I did was to create some more "colorful" prompt templates, add more jokes, and finetune Nous Hermes, an awesome 13b model, on my crazy dataset. The result, well, I have to say, is kind of awesome. Definitely not perfect, but this is the true proof of the concept, an idea I had for a long time: Personality and Memory are trained.
![alt text](https://github.com/SH2318/Emma23/blob/main/img/badcomedian20step.png)
June 24th:\
Today is the day to pivot and reignite my passion. I decided to create some sort of Character Creator for LLMs where you can turn your character design into a chat-based dataset and use it to finetune a model. I named the GitHub repo "LLM-Character-Lab".
As always, every cool idea is usually already done. Character.ai, a "full-stack AI company", on the surface seems to have a platform that renders my idea pointless. However, after looking through their [documentation](https://book.character.ai/character-book/how-to-quick-creation), it seems that their "characters" are simply few-shot or zero-shot descriptions. It is unlikely that a few-shot instruction can outperform my method in the expressiveness of personality and self-awareness. There are of course a bunch more websites similar to this one, as well as Replika (I don't really like what they are doing). But none of them directly collides with my idea. So it's settled, I will make a tool for creating chatbots with complex personalities, and it's going to be *legendary*!\
Phase Three, The End. And the beginning.

#### Phase Four - Prototyping
LLM Character Lab - functionalities:
- A design page for filling in information for the character and packing the information into a dataset.
- A settings page instead of ~~A Main menu with options to open an existing project, create a new one, or go to the settings page.~~
- A chat page, and a chat settings section.
- Keeping it simple for now.

##### Step 1 - Prototype the design page Layout.
##### Step 2 - Create an initial design template.
##### Step 3 - Add functionality of turning design into a dataset.
##### Step 4 - Experiment with the viability of the generated dataset.
##### Step 5 - Continue improving.

2023/06/27\
In the past two days, I learned the Gradio library and built a prototype of the LLM-Character-Lab. Hit a few walls in the process, realizing that I may have been pushing the WebUI a bit too far for a completely modular system, so I went for a different design in the end. So far the app is more like a dataset editor, but I'm hoping to add more functionality to it. I may never actually release the app, we will see how it goes. But my vision is to create an open-source app for developing and sharing datasets, to create a community that shares datasets and templates for training role-playing AIs or even more.
The below image is a simple demonstration of the prototype:
![alt text](https://github.com/SH2318/AGI-stuff-Summer2023/blob/main/img/prototype_demo_230627.png)

Currently, I finished the first 3 steps, which means it is time to move on to step 4, which is to create a dataset using the prototype and use it to finetune a model. I actually had a pretty good idea a few days back, which is to use the [personality test site](https://www.16personalities.com/free-personality-test) as a baseline and use characters.ai to generate stylized responses to the test questions, with some human adjustments of course, to create a style + knowledge representation of character personality. I have decided to start with the famous Tony Stark, aka Iron Man, an iconic character. It would be pretty fun to bring him to life.

2023/06/29\
So um, GitHub is down right now, apparently. I guess I will have to learn about how to train yolov8 a bit later. Thought that I might as well use the time to document what I have been doing lately.\
As mentioned above in the last update, I just finished a prototype of my dataset creation tool, and the next step was to test whether or not my idea works by bringing Tony Stark back to life. So I spent a day, rewatching The Avengers while writing a dataset based on the MBTI personality test questions. And by writing I mean simply asking Tony Stark on character.ai a bunch of questions and picking out the best results. By the end of that day, I had all 60 questions answered and went to bed happily. The next morning, I loaded up a 3090 instance on vast.ai, bumped into another compatibility issue with packages as usual, then trained 2 adapter models based on Nous-Hermes-13b.\
And here is our lovely Tony *Stank* AI. It's Stank because he is a little more annoying than in the movies:
![alt text](https://github.com/SH2318/AGI-stuff-Summer2023/blob/main/img/tony_stank.png)

In the demo, the only information I gave to the model is his name. Because the identity of Iron Man, the billionaire playboy Tony, is already baked into "You:". Which is pretty interesting to think about.\
To me, this is an absolute success. I mean, I got what I consider a pretty great result from such a small dataset. It makes me think about the implications, we could have a community sharing and mixing characters, creating detailed backgrounds and a sense of identity for LLM models. I think some really interesting things can be done here. Of course, I'm just a 19-year-old kid, I probably should not be thinking too big, just focus on getting my degree first I guess.
Back to my little prototype app. I want to have a chat WebUI running locally while the inference takes place in the cloud. I had a week-long project a month ago called Slingshot that did exactly that. It launches a vast.ai instance automatically and then creates a connection between the local code and the inference script that runs in the cloud. The key is to automate everything. This time, I want to use the text-generation-webui to handle the inference, and run it on runpod.io instead. Upon initial testing, I was able to launch instances with TCP ports and specified docker images through python code. But a number of issues remain:\
-- I can't seem to get the ip address through code.\
-- Text-generation-webui only supports generation and loading models with its API. Downloading models is not supported.\
-- I can't seem to connect with ssh using the python library paramiko.\
There are probably fixes to these issues that I'm not seeing, but this time I want to go with a different approach. My first thought is to use the selenium python library to do all the setup on the runpod website like a human would do. But then I thought if I'm going to automate all the clicking, why not do it with an AI agent? It would be so much more interesting!
So here I am, trying to train YOLOv8, an object detection/segmentation model. This should be fun!\

~~### Phase Five - Droid Work for Droids~~
~~Right now, my goal is to automate some of the processes of launching AI models with, well, more AI. First thing first, I gotta do some experiments!~~

### Phase Five - The Ambition & The Dream
YOLOv8 is super fun!
![alt text](https://github.com/SH2318/AGI-stuff-Summer2023/blob/main/img/img6.jpg)
![alt text](https://github.com/SH2318/AGI-stuff-Summer2023/blob/main/img/kitten.gif)\
My original plan was to use object detection to find buttons, and then use classification to determine whether or not it is the button we want. However, seeing how cool this model is I really don't want to use it on something so ridiculous as automating button clicking, I want to do more.\
Remember when I said I was going to build a "Character Creator for LLMs"? Well, I'm pivoting again. Almost like I can never finish what I started. But the truth is, I don't know what more to add to that app. But I do know that I started this summer project hoping to build a super awesome virtual assistant/study buddy. By experimenting with YOLOv8, speaker verification, and whisper with diarization yesterday, and by combining everything I have accomplished from the beginning of the project, I am fully confident that I can build something totally awesome. So let's do this!

- Starting with the "ear". I want to build an ultimate real-time voice input system. With speaker verification and identification, running in real-time, being able to listen to any conversation and way in. I know, quite an ambitious design, I know. But thinking how cool this would be! I have to try!

- If everything goes well,  I will move on to building a chat interface. Experiment with how well my real-time voice input works with LLMs.

- Then, I could try to add Langchain to the mix.

- Next step, explore the idea of giving "vision" to the assistant. Object detection, classification, and text detection are all very interesting to look into.

- Of course, I wouldn't want a boring assistant. I'm going to create a fine tune dataset on personality and self-identity.

- The final touch would be to add text-to-speech capability. SpeechT5 is going to be my default pick. I will definitely add Eleven Labs support. Also, Meta VoiceBox could be added when it releases.

### Phase Six - The Ultimate Voice Input System
Today is July 3rd. In the past two days, I built an audio transcription tool with speaker diarization and word-level time stamps and a real-time voice input system with speaker verification. Using state-of-the-art models such as faster-whisper, wev2vec2, and pyannote-audio models. At a point I tried to combine the two systems, making a real-time transcription tool. [see videos in /img]\
However, the problem with such a system is that it requires a lot of VRAM and still takes quite a bit of time to process. I had to put half of the models on CPU because I only had 6GB of VRAM on my 3060. So in the end, I decided to chase the real-time stuff, because, in the end, I'm building this system for my AI assistant.\
This morning, I added the feature to transcribe long speeches in real-time and push existing transcription to the Gradio chatbot system while the speech is going. My vision for this feature is to have the AI be able to react, understand, or even interrupt conversations in real time. Anyways, as of this point, I have a working real-time voice input system that can recognize my voice implemented in a Gradio app. I'd say great success! And time to move on to the next step, implementing our sassy language model into the app.

### Phase Seven - The Pit
It's been a while since I did the last update. I've got to admit, the past few days have been pretty rough. Kept fixating on small issues, not being able to sleep well, how did I get here? Well, 4 days ago, I was set on creating a "real-time autonomous agent/personal assistant". I started by reading through the Langchain Docs. Langchain is pretty cool, but I decided to set it aside for now because I'm making the chatbot "autonomous" and I'm not using OpenAi API and their embedding services, so it's better for me to implement everything on my terms with full freedom. In the next two days, I went into full madness mode, building systems, Gradio UI, experimenting with prompts, training, writing a character profile, generating and editing datasets, and all kind of stuff all at once. What did I get in the end? A full chatbot system, with real-time voice input, and semi-automatic thought prompting that drives the AI crazy when you don't respond for a while, a  somewhat robotic speecht5 voice output that creates all kinds of new bugs that I didn't have time to fix. Despite the bugs, it works! But it also makes me really confused about what I'm actually doing. I mean, I can generate datasets, I can do alignment and I have this little idea of making the model understand itself through a question-answering dataset. Or, perhaps a thought-based dataset that could teach a model to think quietly to itself. Or, maybe a time-labeled dataset for the model to have a sense of the past, to understand time, history, and growth. All sorts of crazy ideas. But then I decided to try out Exllama, a backend that increases generation speed as well as context length, and I was amazed. So guess what I did today? Yeah, I tried to GPTQ 4bit quantize my custom model. So I merged stuff, I quantized stuff, and bam! Errors. I can't load the model I worked on for an entire day, I still don't know why, maybe it's because the base model I merged with (TheBloke/Nous-Hermes-13B-SuperHOT-8K-fp16), or maybe it's because I have no idea how to do GPTQ quantization. Who knows? One thing I realized today is that I don't have much to bring to the table. All the stuff I did? The training from my super tiny dataset, the "assistant" app, the real-time voice input system, are all very cool stuff in my opinion, but I can't help to feel that what I'm doing is meaningless, that I'm not being any help to the community. Until I had this idea: What if I give my chatbot 3D avatars from Detroit: Become Human? I know I kind of sound delusional here, I'm not sleeping well. But I also have no idea what I'm doing anymore. I'm in a pit, I make efforts and I do make what I consider "pretty cool stuff". But whatever I do, I just end up sliding back to the bottom, almost like the efforts were all for nothing. I'm not sure if going in this direction will get me end up in another endless rabbit hole but I'm giving it a try. Honestly, what I write today is probably gonna read like bullshit a few days later, I don't know, all I know is I want to do this, and I'm going to do this.

### Phase Eight - The DETROIT experience
In the last update, I said I'm abandoning my real-time conversation chatbot to work on making characters from Detroit: Become Human a reality, and that's exactly what I did next. I bought the game and played for the morning. And I have to admit, it was quite an amazing game. Then in the afternoon, I pulled the 3d models and animations out of the game, made a couple of Python scripts to automate some processes and fix issues with the extracted textures, and messed around with the models in Blender for a bit before going to bed. The next morning, just when I thought everything was going well, I realized, there were more than 24,000 animations. Assuming I take 1 minute to import and examine each animation, it would take more than 16 days with no sleep no nothing just looking at the animation every single minute to look through all the files. I could, perhaps make a blender script to automatically import and then render each animation so it would probably be a little faster for me to find the animations I need, but I just don't think it would be worth my time, not to mention I will have to do the lipsync somehow. So I looked at something else, Metahumans, from Unreal Engine. I spent the rest of that day planning a possible 3D virtual assistant system in UE5, and when I say planning, I actually meant spending a lot of time, way too much time, on setting up Visual Studio with UE5. There were so many problems with compiling that I'm definitely not used to. But by the next morning, I had a basic structure design drawn out, and I was ready to start cranking. Websockets, Mesh to Metahuman, input system, Eleven Labs API, everything is going according to plan and I was getting great results. Until lipsyncing. It was so, so slow! It completely destroys the experience. And where do I get more animations? This is not lifelike at all. Building a perfect 3D virtual assistant in the likeness of Chloe from Detroit: Become Human? Just another mirage when you see it up close, another unrealistic fantasy in my mind. For whoever might be reading this, it must be so frustrating seeing me fail again and again, not sticking to what I already have. Well, I do tend to do that don't I? But I don't really see these as failures, I see them as a way of helping me understand and discover my capabilities while taking a look at the limitation of current technologies. But anyways, I still finished the bot, not as enthusiastically,  just a simple chatbot, leaving out all the extra things that I planned. You can see an example video (Chloeandthestars.mp4) in the img folder. I didn't do much today either, only made a Metahuman version of Kara, slapped it into the chatbot system, and called it a day. What next? I'm not sure. I had an idea of finishing my conversational AI and then filming myself spending a day with it. But I'm not doing it tomorrow. I think I'm just going to focus on selecting courses, and packing things for my flight back to China in a few days. I probably won't have a lot of time to work on AI stuff when I'm there, so this might be the end of my little summer project. I hate to end things on a sad note, a failed project. But I have to say, seeing how much I have learned, grown, and build in the past weeks, this is in no way a failure. Sure it might be hard to explain to other people how much I succeeded with all these "abandoned projects", but I think knowing and remembering what I have gone through and achieved should be all I need.\
![alt text](https://github.com/SH2318/AGI-stuff-Summer2023/blob/main/img/MetahumanKara.gif)

### Phase Nine - A Proper Finale, And the Future Ahead.
I know I said I'm not going to do any more AI stuff, but here I am. I just thought I should record a few video demos of my real-time conversation system, even though I kind of gave up on that. And of course, I couldn't resist making a few adjustments to it before recording anything. One thing lead to another, I spent the last two days making a much better version of the system. Building on my initial design of an almost Behavior-Tree-like "action loop", I made a better UI, and added more features and overall I'm quite proud of it. But it didn't work, at first. It was almost like the models are unable to understand the concept of thinking and just end up agreeing to its thoughts like the user can see what it is thinking or something. But then, after a while of experimentation, I was able to get the result I wanted with TheBloke/Pygmalion-13B-SuperHOT-8K-GPTQ. Although at that point I already removed many of the features I added because I thought they are not working. But still, from a simple "think loop" I have right now, the AI will be able to think to itself, have conversations, and go into standby mode. I also got some pretty hilarious results, see img/Karaandtodd.mp4 and img/AiDeepThoughts.mp4. Overall, this is quite a success. I could keep working on it, I think there are a lot of things that can be improved, and I also have a few ideas for building a possible modular functionality system that will allow the user to give the AI more tools and jobs, such as making plans for you on the calendar and remind you things when the event is near. The possibility here is endless, and this could be the ultimate voice assistant that I have been wanting to create. However, as mentioned in the last update, I probably won't be doing a lot of AI stuff in the next month, I need to spend time with family and relax a little bit. That said, I still have something that I want to do. I want to document this, make my experience into a video. Man, I gotta say this update is terribly written, isn't it? There are a lot of things that I want to express but I don't know how. But I have always been good at making videos, maybe I will be able to explain things in a video better, huh?
