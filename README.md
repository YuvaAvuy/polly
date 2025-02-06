# polly


Policy
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": "polly:SynthesizeSpeech",
      "Resource": "*"
    }
  ]
}
Code:
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Happy Birthday from Yuva!</title>
</head>
<body>
    <h2>🎉 Happy Birthday! 🎉</h2>
    <p>Press the "Magic Button" to hear a special birthday greeting from Yuva!</p>

    <button type="button" id="magicButton">Press the Magic Button</button>

    <script src="https://sdk.amazonaws.com/js/aws-sdk-2.181.0.min.js"></script>
    <script>
        AWS.config.update({
            region: "us-east-1",  
            accessKeyId: "YOUR_ACCESS_KEY_ID",  
            secretAccessKey: "YOUR_SECRET_ACCESS_KEY"  
        });

        const polly = new AWS.Polly();

        document.getElementById('magicButton').addEventListener('click', function() {
            const birthdayMessage = "Happy Birthday from Yuva! Wishing you a day full of joy and happiness.";

            const params = {
                Text: birthdayMessage,
                OutputFormat: "mp3",
                VoiceId: "Joanna"
            };

            polly.synthesizeSpeech(params, function(err, data) {
                if (err) {
                    console.log("Error:", err);
                    alert("Polly encountered an error. Check the console for details.");
                } else if (data.AudioStream) {
                    const blob = new Blob([data.AudioStream], { type: "audio/mp3" });
                    const url = URL.createObjectURL(blob);
                    const audio = new Audio(url);
                    audio.play();
                }
            });
        });
    </script>
</body>
</html>





