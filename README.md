# FFME: *WPF MediaElement Alternative*
[![Analytics](https://ga-beacon.appspot.com/UA-8535255-2/unosquare/ffmediaelement/)](https://github.com/igrigorik/ga-beacon)

*:star:Please star this project if you find it useful!*

*A new porting effort is underway! Please check out <a href="https://github.com/unosquare/ffplaydotnet">FFplay.NET</a>*

## Features Overview
FFME is a close drop-in replacement for <a href="https://msdn.microsoft.com/en-us/library/system.windows.controls.mediaelement(v=vs.110).aspx">Microsoft's WPF MediaElement Control</a>. While the standard MediaElement uses DirectX (DirectShow) for media playback, FFME uses <a href="http://ffmpeg.org/">FFmpeg</a> to read and decode audio and video. This means that for those of you who want to support stuff like HLS playback, or just don't want to go through the hassle of installing codecs on client machines, using FFME *might* be the answer. 

FFME implements additional improvements over the standard MediaElement such as:
- Asynchronous and synchronous frame scrubbing
- Fast media seeking
- Frame-by-frame seeking
- Media properties such as Position, NaturalDuration, SpeedRatio, and Volume (among others) are exposed as dependency properties
- Additional and extended media events 

*... all in a self-contained assembly (dll)*

### Known Limitations
*Your help is welcome!*

- SpeedRatio other than 1.0 should adjust audio pitch. Currently, if SpeedRatio is less than 1.0, there is no audio playback, and if SpeedRatio is greater than 1.0, samples just play faster. This situation can be greatly improved by manually manipulating the samples passed to NAudio.
- (*To be confirmed*) Writing to the Position dependency property from another dependency property may make the source value lose synchronization with the target value.
- (*Nice to have*) It would be nice to implement a method on the control that is able to extract a copy of the current video frame.
- There currently is no support for opening capture devices such as webcams or TV cards. While this is not too hard to do, it is not (yet) implemented in this library.

## Compiling, Running and Testing
*Please note that I am unable to distribute FFmpeg's binaries because I don't know if I am allowed to do so. Follow the instructions below to compile, run and test FFME*

1. Clone this repository.
2. Before you open the solution, please make sure you download the FFmpeg win32-shared binaries from <a href="http://ffmpeg.zeranoe.com/builds/win32/shared/ffmpeg-3.0.1-win32-shared.7z">Zeranoe FFmpeg Builds</a>.
3. Extract the contents of the <code>7z</code> file you just downloaded and locate the <code>bin</code> folder.
4. You should see 3 <code>exe</code> files and 8 <code>dll</code> files. Select and copy all of them.
5. Now paste all 11 files from the prior step onto the following folder (inside the cloned repository): <code>{repositiories root}\ffmediaelement\Unosquare.FFmpegMediaElement\ffmpeg32</code>.
6. Open the solution and set the <code>Unosquare.FFmpegMediaElement.Tests</code> project as the startup project. You can do this by right clicking on the project and selecting <code>Set as startup project</code>
7. Click on <code>Start</code> to run the project.
8. You should see a very simplistic media player. Enter a URL or a path to a file in the textbox at the top of the window and then click on <code>Open</code>.
9. The file or URL should play immediately.
10. You can use the resulting compiled assembly in your project without further dependencies FFME is entirely self-contained. The locations of the compiled FFME assembly, depending on your build configuration are either <code>...\ffmediaelement\Unosquare.FFmpegMediaElement\bin\Debug\Unosquare.FFmpegMediaElement.dll</code> or <code>...\ffmediaelement\Unosquare.FFmpegMediaElement\bin\Release\Unosquare.FFmpegMediaElement.dll</code>

## Using FFME in your Project
*The Unosquare.FFmpegMediaElement.Tests project shows most common usages*

1. Create a new WPF application
2. Add a reference to <code>Unosquare.FFmpegMediaElement.dll</code>
3. In your <code>MainForm.xaml</code>, add the namespace: <code>xmlns:ffme="clr-namespace:Unosquare.FFmpegMediaElement;assembly=Unosquare.FFmpegMediaElement"</code>
4. Finally, create an instance of the FFME control in your <code>MainForm.xaml</code> as follows: `<ffme:MediaElement x:Name="MediaEl" Background="Gray" LoadedBehavior="Play" UnloadedBehavior="Manual" />`

## Thanks
*In no particular order*

- To the <a href="http://ffmpeg.org/">FFmpeg team</a> for making the Swiss Army Knife of media.
- To Kyle Schwarz for creating and making <a href="http://ffmpeg.zeranoe.com/builds/">Zeranoe FFmpeg builds available to everyone</a>.
- To the <a href="https://github.com/naudio/NAudio">NAudio</a> team for making the best audio library out there for .NET
- To Ruslan Balanukhin for his FFmpeg interop bindings generator tool: <a href="https://github.com/Ruslan-B/FFmpeg.AutoGen">FFmpeg.AutoGen</a>.
- To Martin Bohme for his <a href="http://dranger.com/ffmpeg/">excellent tutorial</a> on creating a video player with FFmpeg.

## Similar Projects
- <a href="https://github.com/Microsoft/FFmpegInterop">Microsoft FFmpeg Interop</a>
- <a href="https://github.com/Sascha-L/WPF-MediaKit">WPF-MediaKit</a>
- <a href="https://libvlcnet.codeplex.com/">LibVLC.NET</a>
- <a href="http://playerframework.codeplex.com/">Microsoft Player Framework</a>

## License
- The NAudio portion of this library <code>Unosquare.FFmpegMediaElement\NAudio</code> is distributed under Ms-PL. Please see <a href="https://github.com/unosquare/ffmediaelement/blob/master/Unosquare.FFmpegMediaElement/NAudio/LICENSE.txt">LICENSE.txt</a>.
- Code generated by the FFmpeg.Autogen tool <code>Unosquare.FFmpegMediaElement\FFmpeg.Autogen</code> does not specify a license by the tool's author.
- The source code of the FFME project excluding the items above is distributed under the Ms-PL.
