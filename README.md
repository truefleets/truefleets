import AVFoundation

func checkCameraPermission() {
    let cameraStatus = AVCaptureDevice.authorizationStatus(for: .video)
    switch cameraStatus {
    case .authorized:
        openCamera()
    case .notDetermined:
        AVCaptureDevice.requestAccess(for: .video) { granted in
            if granted {
                self.openCamera()
            }
        }
    case .denied, .restricted:
        print("Camera access denied")
    @unknown default:
        break
    }
}