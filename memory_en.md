### Memory Limitation Configuration

Reason: When we enable request interception, the iOS system will launch a dedicated process to handle network requests. However, the system imposes memory limitations on this process. Specifically, for iOS 15 and above, it can only use up to 50MB, and for iOS versions prior to 15, it can only use up to 30MB. Exceeding this memory limit will result in an interruption and exit of the process.

#### 1. Setting Body Size Limitation

When HTTP requests are modified, all data needs to be collected (and if compressed, uncompressed) before decoding. For example, when modifying JSON, we need to wait for the Body to be fully transmitted before decompressing it, and then decoding it into a dictionary or array for data replacement. In order to avoid memory overflow in the process, we set a maximum value for the Body that can be processed. Once this set value is exceeded, modification will be abandoned (if compressed, the uncompression process will also exit if the threshold is exceeded).

#### 2. Setting Decompression Buffer Size

HTTP can compress the Body in transit to improve transmission efficiency. In modifying the Body, a buffer needs to be pre-set for decompression. We set this value based on the compression ratio of the data. If this value is set too small, incomplete data decompression may occur, resulting in decoding failure; if set too large, memory overflow may occur. In actual testing, the author has found that some JSON files can achieve a compression ratio of up to 13 times.