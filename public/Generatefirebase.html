<?php
// Configuration
$firebaseDatabaseUrl = 'https://epicmodder-in-default-rtdb.firebaseio.com';
$firebaseApiKey = 'AIzaSyAE3looRiv-P2fwAvVmBDw0NmEBMPw-dow';

// Initialize variables
$status = '';
$statusClass = '';
$currentDevice = [
    'id' => '',
    'expiry' => '',
    'deviceNumber' => 0
];

// Handle form submissions
if ($_SERVER['REQUEST_METHOD'] === 'POST') {
    if (isset($_POST['generate'])) {
        // Generate new device ID
        $currentDevice['id'] = generateDeviceId();
        $currentDevice['expiry'] = generateExpiryDate();
        $currentDevice['deviceNumber'] = getNextDeviceNumber();
    } elseif (isset($_POST['upload']) && !empty($_POST['device_id'])) {
        // Upload to Firebase
        $result = uploadToFirebase(
            $_POST['device_number'],
            $_POST['device_id'],
            $_POST['expiry']
        );
        
        if ($result === true) {
            $status = "Device {$_POST['device_number']} uploaded successfully! ID: {$_POST['device_id']}";
            $statusClass = 'success';
            $currentDevice['id'] = '';
            $currentDevice['expiry'] = '';
        } else {
            $status = 'Error: ' . $result;
            $statusClass = 'error';
        }
    }
}

// Get next device number from Firebase
function getNextDeviceNumber() {
    global $firebaseDatabaseUrl, $firebaseApiKey;
    
    $url = "{$firebaseDatabaseUrl}/All_User/Device.json?auth={$firebaseApiKey}";
    $response = file_get_contents($url);
    $devices = json_decode($response, true);
    
    return $devices ? count($devices) + 1 : 1;
}

// Generate random 19-character device ID (starting with 00002)
function generateDeviceId() {
    $firstPart = '00002';
    $chars = '0123456789abcdef';
    $rest = '';
    for ($i = 0; $i < 14; $i++) {
        $rest .= $chars[rand(0, strlen($chars) - 1)];
    }
    return $firstPart . $rest;
}

// Generate expiration date 1-2 days from now (MM-DD-YYYY format)
function generateExpiryDate() {
    $daysToAdd = rand(1, 2);
    $date = new DateTime();
    $date->add(new DateInterval("P{$daysToAdd}D"));
    return $date->format('m-d-Y');
}

// Upload data to Firebase using REST API
function uploadToFirebase($deviceNumber, $deviceId, $expiry) {
    global $firebaseDatabaseUrl, $firebaseApiKey;
    
    $url = "{$firebaseDatabaseUrl}/All_User/Device/Device%20{$deviceNumber}.json?auth={$firebaseApiKey}";
    
    $data = json_encode([
        'device_id' => $deviceId,
        'expired' => $expiry,
        'verification' => false
    ]);
    
    $context = stream_context_create([
        'http' => [
            'method' => 'PUT',
            'header' => 'Content-Type: application/json',
            'content' => $data
        ]
    ]);
    
    $response = @file_get_contents($url, false, $context);
    
    if ($response === false) {
        return error_get_last()['message'];
    }
    
    return true;
}

$nextDeviceNumber = getNextDeviceNumber();
?>
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Device ID Generator</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            max-width: 600px;
            margin: 0 auto;
            padding: 20px;
            background-color: #f5f5f5;
        }
        h1 {
            color: #333;
            text-align: center;
        }
        .container {
            background-color: white;
            padding: 20px;
            border-radius: 8px;
            box-shadow: 0 2px 4px rgba(0,0,0,0.1);
        }
        .form-group {
            margin-bottom: 15px;
        }
        label {
            display: block;
            margin-bottom: 5px;
            font-weight: bold;
        }
        button, input[type="submit"] {
            background-color: #4285f4;
            color: white;
            border: none;
            padding: 10px 15px;
            border-radius: 4px;
            cursor: pointer;
            font-size: 16px;
            width: 100%;
            margin-top: 10px;
        }
        button:hover, input[type="submit"]:hover {
            background-color: #3367d6;
        }
        #status {
            margin-top: 10px;
            padding: 10px;
            border-radius: 4px;
        }
        .success {
            background-color: #e6f4ea;
            color: #0d652d;
        }
        .error {
            background-color: #fce8e6;
            color: #c5221f;
        }
        .id-display {
            background-color: #f0f0f0;
            padding: 8px;
            border-radius: 4px;
            font-family: monospace;
            margin: 5px 0;
            word-break: break-all;
        }
        .info-box {
            margin-top: 20px;
            padding: 15px;
            background-color: #f8f9fa;
            border-radius: 4px;
            border-left: 4px solid #4285f4;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Device ID Generator</h1>
        
        <form method="post">
            <div class="form-group">
                <label>Next Device Number:</label>
                <div class="id-display">Device <?php echo htmlspecialchars($nextDeviceNumber); ?></div>
            </div>
            
            <div class="form-group">
                <label>Generated Device ID:</label>
                <div class="id-display">
                    <?php echo !empty($currentDevice['id']) ? htmlspecialchars($currentDevice['id']) : 'Click Generate to create'; ?>
                </div>
                <input type="hidden" name="device_id" value="<?php echo htmlspecialchars($currentDevice['id']); ?>">
                <input type="hidden" name="device_number" value="<?php echo htmlspecialchars($nextDeviceNumber); ?>">
            </div>
            
            <div class="form-group">
                <label>Expiration Date:</label>
                <div class="id-display">
                    <?php echo !empty($currentDevice['expiry']) ? htmlspecialchars($currentDevice['expiry']) : 'Will be generated'; ?>
                </div>
                <input type="hidden" name="expiry" value="<?php echo htmlspecialchars($currentDevice['expiry']); ?>">
            </div>
            
            <input type="submit" name="generate" value="Generate Device ID">
            <input type="submit" name="upload" value="Upload to Firebase" <?php echo empty($currentDevice['id']) ? 'disabled' : ''; ?>>
        </form>
        
        <?php if ($status): ?>
            <div id="status" class="<?php echo $statusClass; ?>"><?php echo htmlspecialchars($status); ?></div>
        <?php endif; ?>
        
        <div class="info-box">
            <h3>Information:</h3>
            <p>Each generated device will have:</p>
            <ul>
                <li>Unique 19-character device ID (starting with 00002)</li>
                <li>Expiration date 1-2 days from now (MM-DD-YYYY format)</li>
                <li>Verification status always set to false</li>
            </ul>
        </div>
    </div>
</body>
</html>