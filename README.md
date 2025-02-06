# bg-remover.github.io<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>BG Remover Pro</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            max-width: 1200px;
            margin: 0 auto;
            padding: 20px;
            background-color: #f0f2f5;
        }

        .container {
            text-align: center;
        }

        .upload-section {
            border: 2px dashed #ccc;
            padding: 40px;
            margin: 20px 0;
            border-radius: 10px;
            background: white;
        }

        .upload-btn {
            background-color: #4CAF50;
            color: white;
            padding: 15px 30px;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            font-size: 16px;
            margin: 10px;
        }

        .preview-area {
            display: flex;
            justify-content: center;
            gap: 20px;
            flex-wrap: wrap;
            margin-top: 30px;
        }

        .preview-box {
            width: 400px;
            height: 400px;
            border: 1px solid #ddd;
            border-radius: 8px;
            overflow: hidden;
            background: white;
            position: relative;
        }

        #imagePreview, #videoPreview {
            max-width: 100%;
            max-height: 100%;
        }

        .processing-overlay {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0,0,0,0.5);
            display: none;
            justify-content: center;
            align-items: center;
            color: white;
        }

        .download-btn {
            background-color: #007bff;
            color: white;
            padding: 10px 20px;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            margin-top: 10px;
            display: none;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Background Remover</h1>
        <div class="upload-section">
            <button class="upload-btn" onclick="document.getElementById('fileInput').click()">
                Upload Image
            </button>
            <button class="upload-btn" onclick="document.getElementById('videoInput').click()">
                Upload Video
            </button>
            
            <input type="file" id="fileInput" accept="image/*" hidden>
            <input type="file" id="videoInput" accept="video/*" hidden>
        </div>

        <div class="preview-area">
            <div class="preview-box">
                <div class="processing-overlay" id="imageProcessing">
                    Removing Background...
                </div>
                <img id="imagePreview" alt="Image Preview">
            </div>

            <div class="preview-box">
                <div class="processing-overlay" id="videoProcessing">
                    Processing Video...
                </div>
                <video id="videoPreview" controls></video>
            </div>
        </div>

        <button class="download-btn" id="downloadImage">Download Image</button>
        <button class="download-btn" id="downloadVideo">Download Video</button>
    </div>

    <script>
        // Image Handling
        document.getElementById('fileInput').addEventListener('change', function(e) {
            const file = e.target.files[0];
            const preview = document.getElementById('imagePreview');
            const processing = document.getElementById('imageProcessing');
            
            if (file) {
                const reader = new FileReader();
                reader.onload = function(e) {
                    preview.src = e.target.result;
                    processing.style.display = 'flex';
                    
                    // Simulate background removal processing
                    setTimeout(() => {
                        processing.style.display = 'none';
                        document.getElementById('downloadImage').style.display = 'inline-block';
                    }, 2000);
                }
                reader.readAsDataURL(file);
            }
        });

        // Video Handling
        document.getElementById('videoInput').addEventListener('change', function(e) {
            const file = e.target.files[0];
            const preview = document.getElementById('videoPreview');
            const processing = document.getElementById('videoProcessing');
            
            if (file) {
                preview.src = URL.createObjectURL(file);
                processing.style.display = 'flex';
                
                // Simulate video processing
                setTimeout(() => {
                    processing.style.display = 'none';
                    document.getElementById('downloadVideo').style.display = 'inline-block';
                }, 3000);
            }
        });
    </script>
</body>
</html>
