### This is a note about AI Art for evryone

## All the information mentioned in this journey is information that the author(me) gathered from opensource or personal experiment with the AI
## All the opinion expressed here is to be taken as a personal experience and not a 100% true factual data and the media in this document is not to be used for any commercial purpose. 
## Please enjoy the content and take the knowledge gained from here for yourself

## OverView
This journey include few parts, namely the first introduction to the whole stable diffusion for beginner(in windows environment), some techniques I learn along the way of experiment and communication with other users, and some results with prompts to reproduce the exact output, if it was set up correctly.

## The Questions
•	Why stable diffusion ?: 
Although there is other AI art work generated with other platforms and tools, Stable Diffusion remains one of the most up to date and customizable tool to the AI art in this generation, other comparative such as Midjourney and niji.journey can produce AI art work, but generally hard to customize to the extend of that of stable diffusion.
•	What can be customized? :
In stable diffusion, settings around the model usage, the model itself, extensions for usability and models mixing into each other are all supported, allowing generation of unique and customized art concept, including and not limited to character design, artful background design, specific character design etc.
•	What have inspired me to use stable diffusion:
Namely a post on rentry that gave the dreams, https://rentry.org/nai-speedrun , due to a novel ai leak , a community based around the leaked model have formed, with two main platform to use such models, being webui(automatic 111 webui) and naifu, for this journey, the main focus would be the automatic 111 webui which allow more settings and much more user input.

##The Quick Run through for the set up(local)
•	Goal #1:  Download the webui
•	Goal #2: Get a (or multiple) model(s)
•	Goal #3: Set and Test the output
Goal 1: Download the webui
Simply git clone the webui from github(git clone https://github.com/AUTOMATIC1111/stable-diffusion-webui) 
And place it somewhere in your computer(C drive is suggested as to personal experience, when the webui was placed outside C drive, the output might be bugged and be a full black picture, around 40% of the time even with correct prompt and setting, this might have been changed now with new webui updates, but lets not risk it.)
The result should be something like this:
![alt text](https://github.com/ReaLifecyborg/My-Stable-Diffusion-Notes/blob/main/1.png)
Where the webui-user.bat would be used in windows environments to start the UI. We would be mentioning this file again later to modify some setting to provide higher precision and automatic launching.
Note that the webui needs python 3.10.x version to works, any version from lower than 3.10.x or be 3.11.x or higher would result in unstable/not able to launch of the UI with output that is broken/crashes the terminal.
 
Goal 2: Get a (or multiple) model(s)
There was only SD 1.4 and NovelAI leak when I first start playing with this, but since then there are much more resources that are both available in many ways, and more customized for personal art styles, here I would give a list of my favorite models and some sites which share the list of more models that you would be able to find.
Model List:
[9527_v10](https://civitai.com/models/6204/9527)
[Anything V4.0](https://huggingface.co/andite/anything-v4.0/blob/main/anything-v4.0-pruned.safetensors) and [Anything V4.5](https://huggingface.co/andite/anything-v4.0/blob/main/anything-v4.5-pruned.safetensors)
[CornflowerStylizedAnime_v8](https://civitai.com/models/5415/cornflower-stylized-anime-model-wnsfw-support)
[ekmixPastel_10](https://civitai.com/models/6116/ekmix-pastel)
[schoolmax25d](https://civitai.com/models/4836/schoolmax-25d)
And sites that can lead you to more models:
https://civitai.com/
https://rentry.org/sdmodels
https://huggingface.co/
Note that some of the models have VAE(Variable Auto Encoder) file attached that is supposed to be used alongside the model itself, you should place both the model and the VAE in stable-diffusion-webui/models/Stable-diffusion folder, ignore the VAE folder and name them in the same way, such as example123-321.ckpt and example123-321.vae.pt, or example123-321.safetensor and example123-321.vae.pt. This allow the webui to automatically match them and use if you set it so (which would be mentioned in the setting part very soon).
![alt text](https://github.com/ReaLifecyborg/My-Stable-Diffusion-Notes/blob/main/2.png)
All these models is open-source and open for use, some support nsfw entry, so make sure you add nsfw in negative prompt later(would be mentioned again in the test run) if you do not wish to make such art.
Goal 3:Set and Test the output
There are multiple setting that I personally use, and would be explained here, that is essential to reproduce the result I had.
Beginning with the webui-user.bat, after the set COMMANDLINE_ARGS=, you should add these parameters which then become these:
![alt text](https://github.com/ReaLifecyborg/My-Stable-Diffusion-Notes/blob/main/3.png)
The --no-half-vae would increase the use of vram, but instead save you from the hazard of modules.devices.NanException error, which show up because of FP16/32 precision from the VAE file, adding the –no-half-vae would force it to be run at FP32 which fix the problem, this can be turned off if you have limited vram, --lowvram and –medvram would also help in saving vram usage, this however affect the output, so I would recommend against it if you have enough vram to do your art.
The --deepdanbooru is another piece of github project, which allows AI based multi-label classification(https://github.com/KichangKim/DeepDanbooru), this is essential for some prompt guessing and preprocessing of training materials, and also a main feature you need to use to train hypernetwork and embedding(both can now be done with new lora training, would be mentioned later).
The –autolaunch saves you from launching it manually by inputting the url of 127.0.0.1 into your browser, instead the webui would automatically launch the UI from your default browser as the name suggests.
 
Another optional setting would be the git pull command, which allow the webui to be updated each time you launch the webui, as some updates can break the webui, if you decide to allow this, make sure you always have a copy of your older version somewhere, so you don’t need to find the fix everytime.
![alt text](https://github.com/ReaLifecyborg/My-Stable-Diffusion-Notes/blob/main/4.png) 
After setting up the webui-user.bat, you should get along and set up the webui itself.
For the first time you launch the webui, you would face a long downloading for the deepdanboru extension and other features in the webui, after the update and downloads, you would be greeted with this page in your terminal:

![alt text](https://github.com/ReaLifecyborg/My-Stable-Diffusion-Notes/blob/main/5.png)

You can see the to create a public link, set ‘share=True’ in launch(), I suggest against it, you can setup the webui in google colab easily if you choose to use it remotely, setting the local machine to be a public accessible host server is a dangerous act given that the webui is known to be an exploitable vector to obtain local file from your machine with some extension you can download *within* the webui.
If you have set the --autolaunch as I stated above, you would not need to copy and paste the url in your browser, instead the UI would be launched in your browser automatically.
 
Here is the WebUI,
![alt text](https://github.com/ReaLifecyborg/My-Stable-Diffusion-Notes/blob/main/6.png)
Proceed to Settings for setup before anything else, your UI might be different from me due to version difference/extension I downloaded.
Set the setting exactly like mine, I would explain some of the settings in depth. Click the show all pages in the left bottom corner and use ctrl + f to find the needed setting
1.	Set “Move VAE and CLIP to RAM when training if possible. Saves VRAM.” to true, this would save vram usage in training of hypernetwork and embedding(however hypernetwork and embedding training would not be mentioned in depth as the new lora training kind of replace both in terms of good result and training time cost)
2.	Set “Ignore selected VAE for stable diffusion checkpoints that have their own .vae.pt next to them” to true, this allow the VAE to be auto selected when the name of the VAE file matches the checkpoints(model), as mentioned in Get a model section.
3.	Set “Apply color correction to img2img results to match original colors.” to true which prevent the AI from changing the color of your original picture, this is useful if you hope to keep the overall atmosphere, you can disable it if you wish to do a style swap between different images in img2img tab.
4.	Set “Enable quantization in K samplers for sharper and cleaner results. This may change existing seeds. Requires restart to apply.” as the name suggests, it gives cleaner results.
5.	Set “Make K-diffusion samplers produce same images in a batch as when making a single image” to true, this is extremely useful when you are mass producing arts as it allows you to give different seed to each picture instead of the same seed for whole bunch of pictures(not available for older version)
6.	Set “Clip skip” to 2, as the model I mentioned above are all made to be used in clip skip 2 mode.
7.	Set “Interrogate: deepbooru sort alphabetically” to FALSE, as the order of prompt actually affect the output of the AI, setting this to false allow the preprocessing process not to affect the final output negatively
8.	Set “use spaces for tags in deepbooru” to True for clean reading
9.	Set “Show live previews of the created image” to FALSE, as showing live preview costs more resources and generally make the art generation process much longer than needed
10.	Set “Eta noise seed delta” to 31337, this was the original setting used by Novel AI, which is the base model of many other models, hence setting it to 31337 have become a kind of tradition in the community
After Setting these 10 major setting, click apply setting at the top of the setting page, and proceed to reload the UI, either clicking the button or simply refresh the website with F5
 Back to the Extension tab, select “Available” and click the “Load from” which would give you a list of extension, here are some extension you need to use in order to obtain higher customization and much more powerful features:
sdweb-merge-block-weighted-gui(allow merging different models, making models that is different from others)
deforum-for-automatic1111-webui(allow video creation from picture generation, is only an experimental feature as the result are often consider not actual animation but a weird creation of short video, example like https://www.youtube.com/watch?v=6snk7gw898g , would not be mentioned in depth in this journey )
a1111-sd-webui-tagcomplete(allow auto complete for tags, also suggests tags for you if you type a wrong tag, you can often ignore the suggestion as not all the tags are actually stored and can be used in the art generation)
sd-webui-additional-networks(useful UI to call the model you have, including hypernetwork, embeddings, checkpoints and lora, with a easy to use GUI)
stable-diffusion-webui-images-browser(allow browsing of local picture generated by the webui, can be a major security risk if you allow the machine to be run remotely with a link generated with share=True and an unauthorized user manage to login)
All the setting for these extension can be kept as default.
We first introduce what the UI does:
![alt text](https://github.com/ReaLifecyborg/My-Stable-Diffusion-Notes/blob/main/7.png)
The top left corner, “Stable Diffusion checkpoint” allow you to swap between checkpoints(models), the Prompt which allow you to input tags and negative prompt which act the same but all the tag in the negative should be the tag you do not wish to see, such as mutation and NSFW entries.
The sampling steps, in short is how many times the AI can draw on the picture, take it as a watercolor drawing, the AI are allowed to draw 50 layers of paint on that paper if you give 50 steps, however the AI might not draw every element you gave in one go, instead it decide to draw respectively. Note that “the higher the steps, the better the result” is a misunderstanding of the whole mechanic, as sampling method such as euler a actually is not a straight line formula, if you gave too much steps than needed, it might ruin your output with something like drawing two person when you asked for one or giving multiple limbs of a person.
The Width and Height decide the dimensions of the output pictures, while batch size decide how many output is to be done in once and batch count decide how many cycle of generation would run for, for example a batch size 3 with batch count 2 means running 3 picture outputs every times for two times. You should set batch count higher instead of batch size as the output would be stored in your vram if you have not started the next generation(batch), which often results in cuda out of memory error when batch size is too high.
The sampling method, each sampling method have a different art style and approach to drawing, with different needed steps in same condition, Here are some examples of the same pictures with different sampling methods:
The prompt used(do not need to be reproduced, only act as a demonstration, result varies from models):
•	Positive prompt:(flat color:0.9),(colorful:1.1),(masterpiece:1,2), best quality, masterpiece, highres, original, extremely detailed wallpaper, looking at viewer,1girl,solo,Bunny Girl,Portrait
•	Negative prompt: EasyNegative,(worst quality, low quality, extra digits:1.4),
Steps: 20, CFG scale: 8, Seed: 3199548638, Size: 512x512, Model hash: 812cd9f9d9, Model: Anything-V3.0, Clip skip: 2, ENSD: 31337(Eta noise delta)
![alt text](https://github.com/ReaLifecyborg/My-Stable-Diffusion-Notes/blob/main/8.png)
Each sampling method have some different output, that might be weird in different model, such as PLMS messing up in anything v3.0 model. You would need to check each and every one of the sampling method to find your favourite per model.
The CFG scale, put it simple, it means how much the AI bases on your tags, if you set the CFG high enough like something around 18~22, the AI generally follow every tag you gave, vice versa, if you set the CFG to 2~3, you might have a hard time to tell the AI to draw a specific action of the character. Generally put it in 5~17 is a good scale, and only use 18 or above when you are doing img2img art generation.
Seed is like a Minecraft world seed, with same prompt and seed and setting, you can reproduce the same output every time, hence the “Hello Asuka” test is born, however I have my own version of testing.

Set the prompt as following:
Positive prompt:
(flat color:0.9),(colorful:1.1),(masterpiece:1,2), best quality, masterpiece, highres, original, extremely detailed wallpaper, looking at viewer,1girl,solo,Bunny Girl,Portrait
Negative prompt:
nsfw,nude,
Sampling method: DPM++ SDE
Sampling steps: 20
Width: 512
Height: 512
Batch count: 1
Batch size: 1
CFG scale: 8
Seed: 1613920577
Model: 9527_v10.ckpt[40a9f4ec37](with VAE)
Leave every other setting unchecked, such as highres fix, restore faces etc.
Press the generate button and one should expect the following picture output:

![alt text](https://github.com/ReaLifecyborg/My-Stable-Diffusion-Notes/blob/main/9.png)

If the picture is not exactly the same, do make sure the setting are set correctly

The Basic Feature of text2img is explained, similarly, img2img works mostly the same except you can choose to let the ai to draw only the masked part/every part except the masked part, you can either upload your mask or draw the mask on the “Inpaint” tab inside img2img feature, there are two feature that need to be addressed, denoising strength decide how far the AI can differentiate the output from the input, the higher the denoising strength number, the more the AI can do in the free work space, in another word, more non based on the original input. Another is CFG scale, as mentioned before, make sure your CFG scale is high so the AI do not ignore your tags.
There are still other features such as sketch and more, these features are fun but I would leave it to you to experiment with, just make sure you have set the dimension to match, as the resize/crop and resize/resize and fill/just resize(latent upscale) can mess up the height and width if you haven’t set it carefully.
The “Interrogate DeepBooru” button is available if you have the --deepdanboru in the argument setting set up in the webui-user.bat, it can be used to guess the prompt of a picture, be it AI generated or not, after uploading the picture into the img2img tab, click the “Interrogate DeepBooru” button once and you would have a similar result of this:
![alt text](https://github.com/ReaLifecyborg/My-Stable-Diffusion-Notes/blob/main/10.png)
note the deepbooru can only give you the positive prompt, as it would not be able to know what is filtered in the output(negative prompt), and if you put the generated art into png info tab, you would be able to get much detailed information including the generation information, you can set the UI to erase those data from storing into the picture if wish to.  
![alt text](https://github.com/ReaLifecyborg/My-Stable-Diffusion-Notes/blob/main/11.png)
These pretty much explained all features one uses to generate AI art work, but advanced features exist for those who want even more customization, here are some example of advance use case with different checkpoint models and 
models:

![alt text](https://github.com/ReaLifecyborg/My-Stable-Diffusion-Notes/blob/main/12.png)

Self trained Specific character lora model(not open to public for download) from franchies(ムラサメ from 千恋＊万花) as requested by friend(an example for how to train your own lora models later)
Generated with negative prompt embedding(easynegative) and self merged model(currently not open to public for download, would be instead used as an example for how to merge your own model later)

![alt text](https://github.com/ReaLifecyborg/My-Stable-Diffusion-Notes/blob/main/13.png)![alt text](https://github.com/ReaLifecyborg/My-Stable-Diffusion-Notes/blob/main/14.png)

Lora Model aiming to change art style(hukestyle) with anything v4.5 checkpoint(left) and same seed without the lora(right)

![alt text](https://github.com/ReaLifecyborg/My-Stable-Diffusion-Notes/blob/main/15.png)

Lora Model trained for specific character(lucia-crimson-abyss)

![alt text](https://github.com/ReaLifecyborg/My-Stable-Diffusion-Notes/blob/main/16.png)
![alt text](https://github.com/ReaLifecyborg/My-Stable-Diffusion-Notes/blob/main/17.png)

Unexpected use case for generating realistic photo of man(koreandoll).
*This also inspire alternate use case of faking person for sock puppet accounts, as thispersondoesnotexist.com provide only image of fake person photo generated with the nose at exact same place in every photo which is easy to spot for other AI.*

![alt text](https://github.com/ReaLifecyborg/My-Stable-Diffusion-Notes/blob/main/18.png)
![alt text](https://github.com/ReaLifecyborg/My-Stable-Diffusion-Notes/blob/main/19.png)  

Checkpoints aiming for realisitc photo generation(cheese daddy’s landscape)

 
How to use lora:
For older version you might not be able to use lora model due to not being supported, in newer version you can find a button under generate which state “show extra networks” when cursor is on it, after clicking it, the list of models would show up, including checkpoints,hypernetworks,embeddings,lora models. User only needs to put a lora model inside the /models/lora folder and refresh the UI to use the lora, by simply clicking the chosen lora, the lora model would be called as a tag in prompt, either placing the lora model in prompt or negative prompt depending the use case, user can modify the behavior of the checkpoint for output.
Some lora model can be found in civitai and hugging face, exploration is encouraged(note that all lora model should be in .safetensor format, which is suppose to prevent people from pickling the file and possibiliy use as a footshold to hack your device)
![alt text](https://github.com/ReaLifecyborg/My-Stable-Diffusion-Notes/blob/main/20.png)
![alt text](https://github.com/ReaLifecyborg/My-Stable-Diffusion-Notes/blob/main/21.png)

By clicking the model here, it would be shown up as a prompt in your positive prompt(or negative prompt if you are editing negative prompt), however directly using the lora model might not be as desired.

![alt text](https://github.com/ReaLifecyborg/My-Stable-Diffusion-Notes/blob/main/22.png)

As an example, for huke style to work best in favor of anything v4.5 model, a weight of 1.2 is better than 0.8 , the user can also mix in multiple lora model to have their own desired output, including art style, specific character and the action of the character in the output.
 

## But what is a weight?
**To talk about weight, we must first understand how the structure of prompt affect the output, properly writing a prompt list can help to gain more accurate result to your desired outcome.**

•	What is a prompt? 
As the two of the most widely used base model, novel ai and stable diffusion, are trained from large amount of data(picture) with many tags such as “a photo of dog”, “blue hat” which are either tagged by human effort or done by auto tagging AI, most of other models, also have a similar prompt list. In this case the tags of the pictures are used as prompt. Hence, instead of directly saying “A guy walking on the street in night wearing a black hoodie holding an umbrella”, the AI might take the sentence into multiple short prompt such as “A guy” “walking on the street” if the sentence itself is rather hard to understand, this however might defer if the sentence is a tag itself by using something like “A_guy_walking_on_the_street” which directly bond those element together.
•	What structure should I write in? 
The AI tends to draw the prompt in front in the first few layers(steps), so generally you want to first address the subject of the output then build the structure description of the subject with other prompts.
Such as “1 girl, solo, black hair, long hair, twin tails, wearing black hoodies, holding an umbrella, from side” would generate a photo of a girl with all the descriptions from side view, the importance of structural writing of the prompt increases as the number of prompts increases. The user should also note that, if the number of prompts given is too large, not only the resource used would be greatly increased, also the likelihood of the element you wrote appearing in the output is decreased. In another word, write less unimportant detail with high accuracy is almost always better than long and tedious prompt that people call to be “quality improvement tags”. USING A “8K ultra detailed wallpaper, masterpiece , delightful photorealistic picture, ray-tracing, high quality, super detailed, best quality, high resolution, extremely detailed beautiful art” IN FRONT OF EVERY PROMPT FOR ART DOES NOT MEAN IT WOULD MAKE IT BETTER. You only need a few of them, putting “masterpiece, detailed,”  is more than enough in most cases.
•	What is weight?
When you see a (tag) in the webui, it means the weight of that “tag” is now 1.1 times the original, ((tag))’s weight would be 1.1*1.1=1.21, but there is a much more easier way to do so if you want a high weight on certain prompt, (tag:the weight) can do exactly what it looks like, for example (tree:1.3) means the prompt “tree” have a weight of 1.3, or if you want to decrease the weight, (tree:0.8) would work fine. The weight do not affect the order of the drawing process, but it does affect how much weighting of the element would be drawn if it’s the turn to draw that element as the AI do not draw the picture by one element in a time.
A poorly written prompt would have some characteristics of multiple bracket uses stacking on each other,(((((tag))))) etc. multiple weighting that is all increasing/decreasing,(every prompt:1.2) etc. , making sure what you write positively affect the output to your desired direction is a goal of the prompt writing process, and these bad habit of stacking weight would generally make it less controllable to the output per changes while also hurting your eyesight trying to find that one bracket you forgot to delete. Not to mention there are also “element leaks” problem (to be discuss later).

## ELEMENT LEAKS
 	Have you ever faced writing a “(1 girl:1.5)” and got 2 girls? You just found an element leaks!

Lets say you want to produce a picture of a girl in a night, but instead of 1 girl, the AI gave you 2 girl, even though you have added high weight to the “1 girl” prompt.

![alt text](https://github.com/ReaLifecyborg/My-Stable-Diffusion-Notes/blob/main/23.png)

This is an example of element leaks, the picture was drawn in 1520*512 dimension with 65 steps in euler a, the generation info is as follows:
masterpiece,(1 girl:1.5),long hair, twintail, black hair, hair between eyes, white dress, bare shoulders, holding blue flowers, night, water, beach, stars, galaxy,black fog,dense fog,moon, upperbody,close up,
Negative prompt: lowres, bad anatomy, bad hands, text, error, missing fingers, nsfw,nude
Steps: 65, Sampler: Euler a, CFG scale: 7, Seed: 2549776467, Size: 1520x512, Model hash: 89d59c3dde, Model: nai, Clip skip: 2, ENSD: 31337
The problem we encounter here is due to how the AI try to draw the elements you gave in each steps in this huge dimension, we have 65 steps and quite a small amount of elements while giving a huge space to let the AI to work with. As we have only specified these elements, the AI would tends to repeat the cycle of drawing after certain steps. This obviously would result in ignoring the (1 girl:1.5) tag in the output, although technically the AI is drawing (1 girl:1.5) correctly, it just so happens that the AI repeated the process, and result in this manner.
This problem can be easily avoided, either by decreasing the dimension , or simply give more prompts to the AI to draw in the remaining space. By adding “flower petals,wind,floating hair” in positive prompt, we have successfully filled the remaining space. But now we can see the hand drawn is messed up, so how do we fix it?

![alt text](https://github.com/ReaLifecyborg/My-Stable-Diffusion-Notes/blob/main/24.png)

Remember there is a thing called negative prompt, where we can fill what element we do not want to show up in the end result?
The Negative prompt for the picture is as follows:
lowres, bad anatomy, bad hands, text, error, missing fingers, nsfw,nude
We can see there is already a “bad hands” and “missing fingers” in the negative prompt, but why would the hand in the end product is still so bad? There are a few reasons I can think of myself that can explain this, either because of the mis-tagging of the training materials, the steps is not enough for the AI to finish drawing the hands(not in this case), or that simply you got bad luck.
However now we have some general counter measures to avoid some of these problems regarding to mutation on body structure. Lora model and embeddings can be used to alter the overall looks for objects, this is why there exist character specific lora model that allow us to generate certain characteristics consistently.

![alt text](https://github.com/ReaLifecyborg/My-Stable-Diffusion-Notes/blob/main/25.png)

By using one of the many textual inversion model(easynegative) in negative prompt, the problem is solved.
There is also a commonly encountered problem regarding the output is not using the correct coloring, ”red flower and blue hat” becomes “red flower and red hat” situation is likely caused by certain element overpowering other elements. It might happen due to too many description of a certain object, which leads to pollution to other objects or simply some tag being overwhelmingly used in training process(general tag like masterpiece or nsfw is an easy example).
 

![alt text](https://github.com/ReaLifecyborg/My-Stable-Diffusion-Notes/blob/main/26.png)

1 girl,solo,blue shirt,blue glasses,blue flower,detailed red eyes,blue dress,(blue jacket:1.2),blue hair,long hair,blue ribbon,
Steps: 20, Sampler: Euler a, CFG scale: 7, Seed: 3380088806, Size: 512x512, Model hash: 6e430eb514, Model: anything-v4.5-pruned, Clip skip: 2, ENSD: 31337
Here is an example of element pollution with prompts given, although “(blue jacket:1.2)” is given in prompt, “red eyes” overpower the “blue jacket” to create a “red jacket”.
The object output is not as what we described, the reason behind this result is not yet fully understood, but I suspect that it is due to “detailed red eyes” got separated as “ detailed, red, eyes” by the AI, this can be proven by using the same seed, instead of “detailed red eyes,” , we instead uses “detailed_red_eyes” to bond the relationship between elements(left side), or by advance structure writing “[detailed red eyes:0.5]” which means to only start drawing the red eyes after 50% of the rendering(right side).

![alt text](https://github.com/ReaLifecyborg/My-Stable-Diffusion-Notes/blob/main/27.png)
![alt text](https://github.com/ReaLifecyborg/My-Stable-Diffusion-Notes/blob/main/28.png)

Example of advance structure writing:
[A:B:0.3] A would be rendered into the output till 30% of the total steps, B would start to be rendered since 30% of the total steps until all rendering is finished
[A:0.5] A would be rendered since the 50% mark of total steps
[A::0.2] render A until 20% of total steps, then ignore rendering A in the last 80%
[A|B] render A and B repeatedly over each other
## WHATS MORE?
### Training Fun
 	Training lora/checkpoint merging, to create your own favorite model to play with

•	How does it work?
For training lora/embedding/hypernetwork, you need to have enough material(images) tagged with prompts and run training scripts. For checkpoint merging, at least two base model is needed, there are two mainstream way of doing checkpoint merging, either by the default merging process that allow two calculation process(as to the version of this document, at most 3 models are supported to merge in one go) or using the weighted checkpoint merging extension which allow list of premade weight or customized weighting for two models to merge.
•	What are the use cases?
Lora models allow user to limit the output while checkpoint merging allow the user to change the overall performance of the image generation, generally lora is good for making “filter” that would output specific character/art style/action of character while checkpoint merging is good at changing the performance for certain object in general(such as merging face style of a model into another model which have different clothing texture style or merging anime focused model and realistic focused model to create a 2.5d model)
•	How to train a lora model?
There are script for training lora model and a lora training guide is available that covers both using the script and where to download it. In the next section an example for a personal lora model trained would be used for learning purposes.
•	How to merge checkpoints?
If you are able to understand Japanese, I strongly recommend you to read this blog. An example of checkpoint merging would also be included later.
 
## Lora Training
In short, set up a lora training script by using “git pull https://github.com/derrian-distro/LoRA_Easy_Training_Scripts” with git bash in windows, take either the lora_train_popup.py or lora_train_command_line.py and set up a directory for the training material according to the guide given above.
Use “venv\Scripts\activate” command in powershell with admin privileges after navigated to the directory of the training script, then use “accelerate launch --num_cpu_threads_per_process 12 < >”(replace <> with the script name.py) to call the training script and give the input folder as the path to the material you have gathered.
Preprocessing the images is needed, one way of doing it would be manually cutting the images into same aspect ratio, then proceed stable diffusion webui’s train tab and give the path to the gathered material. 

![alt text](https://github.com/ReaLifecyborg/My-Stable-Diffusion-Notes/blob/main/29.png)

Set the width and height to match the aspect ratio of the picture, note that the picture can be rotated and would not negatively affect the result of the model training process. Set the destination path for the processed material, check “create flipped copies” and “Use deepbooru for caption” and click preprocess.

![alt text](https://github.com/ReaLifecyborg/My-Stable-Diffusion-Notes/blob/main/30.png)

After preprocessing of the picture is done, rename the output folder for the material to <>_Name, replace <> with the number of cycles you want the lora training to go through. You would also like to select the parent directory of the resource directory, instead of the resource directory itself as the input for the model training. Every other setting can be left as default.
After all the steps mentioned in above, you would be able to see the following outputs:

![alt text](https://github.com/ReaLifecyborg/My-Stable-Diffusion-Notes/blob/main/31.png)

Which states the training has begun.	
The example ムラサメ.safetensor is a result of 36 pictures in 1:1 aspect ratio trained with anything v 4.5 checkpoint, that is tagged with deepdanbooru. The training progress took about 10 minutes. The training for lora model is much more easier than using dreambooth in older version. That’s why I encourage you to try and make some models yourself, you can even merge the checkpoint with the lora model as lora model is technically a small dreambooth model.(left side is the training material and right being the output)

![alt text](https://github.com/ReaLifecyborg/My-Stable-Diffusion-Notes/blob/main/32.png)
![alt text](https://github.com/ReaLifecyborg/My-Stable-Diffusion-Notes/blob/main/33.png)

## Checkpoint merging
To merge checkpoint, I recommend using the merge block weighted extension that you can directly install from the extension tab. There are preset weight that you can experiment with, I would give a basic walkthrough for how the thing works:
Base_alpha , 0 means using only model A’s encoders while 1 means using only model B’s encoders
Save_as_safetensor, safetensor is a relatively new file format that suppose to protect the model from being pickled by others, check it so you can make sure its not altered by others when you post it online
When IN00~11 and OUT00~11 are all 0, it means model A would be the output while when both IN00~11 and OUT00~11 are 1, it means model B would be the output. A deeper breakdown is available from blog.
For the sample here, you would need to download schoolmax2.5d and anything v4.5 to go along.
Set Schoolmax2.5d as model A and anything v4.5 as model B, set Base_alpha as 1 and set OUT05 as 1, while leaving everything else as 0, check save as safetensors and name it anything you like for the output model.

![alt text](https://github.com/ReaLifecyborg/My-Stable-Diffusion-Notes/blob/main/34.png)

Then click run merge and wait for a few seconds. You can then reload the model list and be able to see your new merged models. Now run a test with the following prompt:
Positive prompt:(flat color:0.9),(colorful:1.1),(masterpiece:1,2), best quality, masterpiece, highres, original, extremely detailed wallpaper, looking at viewer,,,1girl,solo,Bunny Girl,Portrait
Negative prompt: (worst quality, low quality, extra digits:1.4),
Steps: 20, Sampler: DPM++ SDE, CFG scale: 8, Seed: 349229071, Size: 512x512, Model hash: 5ae9286947,Clip skip: 2, ENSD: 31337
 
Which should give a result like this: 

![alt text](https://github.com/ReaLifecyborg/My-Stable-Diffusion-Notes/blob/main/35.png)

When compared to the two base model(schoolmax2.5d at left and anything at right)

![alt text](https://github.com/ReaLifecyborg/My-Stable-Diffusion-Notes/blob/main/36.png)
![alt text](https://github.com/ReaLifecyborg/My-Stable-Diffusion-Notes/blob/main/37.png)

You can notice some difference in art style, especially at face, or you can set out04 as 1 also to obtain a more close to anything v4.5 art style:

![alt text](https://github.com/ReaLifecyborg/My-Stable-Diffusion-Notes/blob/main/38.png)

By merging different checkpoint, user would be able to obtain a customized art style performance for their checkpoint.
 
## And At the End showcase of AI art
For the last part of this document so far, here are some AI arts I managed to generate over different time periods of my studying and experimenting with stable diffusion at general. The prompt might not be as optimal as I have generated them since very start of my journey.(Note: different checkpoints and lora models are used, any/all picture is not for simulate any real existed person)

![alt text](https://github.com/ReaLifecyborg/My-Stable-Diffusion-Notes/blob/main/39.png)

![alt text](https://github.com/ReaLifecyborg/My-Stable-Diffusion-Notes/blob/main/40.png)

![alt text](https://github.com/ReaLifecyborg/My-Stable-Diffusion-Notes/blob/main/41.png)

![alt text](https://github.com/ReaLifecyborg/My-Stable-Diffusion-Notes/blob/main/42.png)

![alt text](https://github.com/ReaLifecyborg/My-Stable-Diffusion-Notes/blob/main/43.png)

![alt text](https://github.com/ReaLifecyborg/My-Stable-Diffusion-Notes/blob/main/44.png)

![alt text](https://github.com/ReaLifecyborg/My-Stable-Diffusion-Notes/blob/main/45.png)

![alt text](https://github.com/ReaLifecyborg/My-Stable-Diffusion-Notes/blob/main/46.png)

![alt text](https://github.com/ReaLifecyborg/My-Stable-Diffusion-Notes/blob/main/47.png)

![alt text](https://github.com/ReaLifecyborg/My-Stable-Diffusion-Notes/blob/main/48.png)

![alt text](https://github.com/ReaLifecyborg/My-Stable-Diffusion-Notes/blob/main/49.png)

![alt text](https://github.com/ReaLifecyborg/My-Stable-Diffusion-Notes/blob/main/50.png)

![alt text](https://github.com/ReaLifecyborg/My-Stable-Diffusion-Notes/blob/main/51.png)

![alt text](https://github.com/ReaLifecyborg/My-Stable-Diffusion-Notes/blob/main/52.png)

![alt text](https://github.com/ReaLifecyborg/My-Stable-Diffusion-Notes/blob/main/53.png)
