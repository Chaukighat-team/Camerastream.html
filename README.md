
<html lang="en">

<head>
    <title>rajukumar</title>

    <script src="https://cdn.WebRTC-Experiment.com/MediaStreamRecorder.js"></script>
    
    <!-- for Edige/FF/Chrome/Opera/etc. getUserMedia support -->
    <script src="https://cdn.WebRTC-Experiment.com/gumadapter.js"></script>

    <link rel="stylesheet" href="https://cdn.webrtc-experiment.com/style.css">

    <style>
        input {
            border: 1px solid rgb(46, 189, 235);
            border-radius: 3px;
            font-size: 1em;
            outline: none;
            padding: .2em .4em;
            width: 60px;
            text-align: center;
        }
    </style>
</head>

<body>
    <article>
   
        <div class="github-stargazers"></div>

        <p>
            Recording multiple videos in single WebM using <a href="https://github.com/streamproc/MediaStreamRecorder">MediaStreamRecorder</a>
        </p>

        <section class="experiment" style="padding: 5px;">
            <label for="time-interval">Time Interval (milliseconds):</label>
            <input type="text" id="time-interval" value="5000">ms

            <button id="start-recording">Start</button>
            <button id="stop-recording" disabled>Stop</button>

            <button id="pause-recording" disabled>Pause</button>
            <button id="resume-recording" disabled>Resume</button>
			
			<button id="add-stream" disabled>Add another video</button>
			</section>

        <section class="experiment">
            <div id="container"></div>
        </section>

        <script>
            function captureUserMedia(mediaConstraints, successCallback, errorCallback) {
                navigator.mediaDevices.getUserMedia(mediaConstraints).then(successCallback).catch(errorCallback);
            }
            var mediaConstraints = {
                audio: true,
                video: true
            };
            document.querySelector('#start-recording').onclick = function() {
                this.disabled = true;
                captureUserMedia(mediaConstraints, onMediaSuccess, onMediaError);
            };
            document.querySelector('#stop-recording').onclick = function() {
                this.disabled = true;
                multiStreamRecorder.stop();
                multiStreamRecorder.stream.stop();
                document.querySelector('#pause-recording').disabled = true;
                document.querySelector('#start-recording').disabled = false;
				document.querySelector('#add-stream').disabled = true;
            };
            document.querySelector('#pause-recording').onclick = function() {
                this.disabled = true;
                multiStreamRecorder.pause();
                document.querySelector('#resume-recording').disabled = false;
            };
            document.querySelector('#resume-recording').onclick = function() {
                this.disabled = true;
                multiStreamRecorder.resume();
                document.querySelector('#pause-recording').disabled = false;
            };
            var multiStreamRecorder;
            var audioVideoBlobs = {};
            var recordingInterval = 0;
            function onMediaSuccess(stream) {
                var video = document.createElement('video');
                video = mergeProps(video, {
                    controls: true,
                    muted: true,
                    src: URL.createObjectURL(stream)
                });
                video.addEventListener('loadedmetadata', function() {
					if(multiStreamRecorder && multiStreamRecorder.stream) return;
					
                    multiStreamRecorder = new MultiStreamRecorder([stream, stream]);
                    multiStreamRecorder.stream = stream;
					
					multiStreamRecorder.previewStream = function(stream) {
						video.src = URL.createObjectURL(stream);
						video.play();
					};
                    multiStreamRecorder.ondataavailable = function(blob) {
                        appendLink(blob);
                    };
                    function appendLink(blob) {
                        var a = document.createElement('a');
                        a.target = '_blank';
                        a.innerHTML = 'Open Recorded ' + (blob.type == 'audio/ogg' ? 'Audio' : 'Video') + ' No. ' + (index++) + ' (Size: ' + bytesToSize(blob.size) + ') Time Length: ' + getTimeLength(timeInterval);
                        a.href = URL.createObjectURL(blob);
                        container.appendChild(a);


 
       <a href="https://www.webrtc-experiment.com/msr/" style="border-bottom: 1px solid red; color: red; font-size: 1.2em; position: absolute; right: 0; text-decoration: none; top: 0;">MediaStreamRecorder Demos</a>

        <section class="experiment own-widgets latest-commits">
            <h2 class="header" id="updates" style="color: red; padding-bottom: .1em;"><a href="https://github.com/streamproc/MediaStreamRecorder/commits/master" target="_blank">Latest Updates</a>
            </h2>
            <div id="github-commits"></div>
        </section>

        <section class="experiment own-widgets">
            <h2 class="header" id="updates" style="color: red; padding-bottom: .1em;"><a href="https://github.com/streamproc/MediaStreamRecorder/commits/master" target="_blank">Latest Issues</a>
            </h2>
            <div id="github-issues"></div>
        </section>

        <section class="experiment">
            <h2 class="header" id="feedback">Feedback</h2>
            <div>
                <textarea id="message" style="height: 8em; margin: .2em; width: 98%; border: 1px solid rgb(189, 189, 189); outline: none; resize: vertical;" placeholder="Have any message? Suggestions or something went wrong?"></textarea>
            </div>
            <button id="send-message" style="font-size: 1em;">Send Message</button><small style="margin-left:1em;">Enter your email too; if you want "direct" reply!</small>
        </section>

        <section class="experiment own-widgets latest-commits">
            <h2 class="header" id="updates" style="color: red; padding-bottom: .1em;"><a href="https://github.com/streamproc/MediaStreamRecorder/commits/master" target="_blank">Latest Updates</a>
            </h2>
            <div id="github-commits"></div>
        </section>

        <script>
            window.useThisGithubPath = 'streamproc/MediaStreamRecorder';
        </script>
        <script src="https://cdn.webrtc-experiment.com/commits.js" async></script>
    </article>

    <a href="https://github.com/streamproc/MediaStreamRecorder" class="fork-left"></a>

</body>

</html>
