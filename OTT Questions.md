# OTT iOS Senior Software Developer Interview Questions & Answers

## Video Streaming & Playback

### Q1: How would you implement adaptive bitrate streaming in an iOS OTT app?
**Answer:** 
Adaptive bitrate streaming automatically adjusts video quality based on network conditions. I would:
- Use AVPlayer with HLS (HTTP Live Streaming) which natively supports adaptive bitrate
- Implement network monitoring using `NWPathMonitor` to track bandwidth changes
- Configure multiple bitrate variants in the HLS manifest
- Monitor `AVPlayerItem.accessLog()` to track quality switches
- Implement custom logic for aggressive or conservative quality switching based on user preferences

```swift
// Example implementation
class AdaptiveStreamingManager {
    private let player = AVPlayer()
    private let pathMonitor = NWPathMonitor()
    
    func setupAdaptiveStreaming(url: URL) {
        let asset = AVURLAsset(url: url)
        let playerItem = AVPlayerItem(asset: asset)
        
        // Monitor network changes
        pathMonitor.pathUpdateHandler = { [weak self] path in
            self?.adjustStreamingStrategy(for: path)
        }
        
        player.replaceCurrentItem(with: playerItem)
    }
}
```

### Q2: Explain the difference between HLS, DASH, and Smooth Streaming protocols.
**Answer:**
- **HLS (HTTP Live Streaming):** Apple's protocol, natively supported on iOS. Uses `.m3u8` playlists and `.ts` segments. Best for Apple ecosystem
- **DASH (Dynamic Adaptive Streaming over HTTP):** Open standard, more flexible than HLS. Uses XML manifests and various container formats
- **Smooth Streaming:** Microsoft's protocol, less common in mobile apps. Uses fragmented MP4

For iOS OTT apps, HLS is preferred due to native support and App Store requirements for streaming content over cellular networks.

### Q3: How do you handle video buffering and preloading strategies?
**Answer:**
Implement a multi-layered buffering strategy:
- **Forward Buffer:** Use `AVPlayerItem.preferredForwardBufferDuration` to control how much content to buffer ahead
- **Preloading:** Implement intelligent preloading based on user behavior patterns
- **Background Downloads:** Use `AVAssetDownloadTask` for offline content
- **Memory Management:** Monitor memory usage and clear unnecessary buffers

```swift
// Configure buffering
playerItem.preferredForwardBufferDuration = 30.0 // 30 seconds
playerItem.canUseNetworkResourcesForLiveStreamingWhilePaused = true
```

## DRM & Content Protection

### Q4: How would you implement FairPlay DRM in an OTT app?
**Answer:**
FairPlay DRM implementation involves:

1. **Certificate Acquisition:** Obtain FairPlay certificate from Apple
2. **License Server Communication:** Implement secure communication with license server
3. **Key Delivery:** Handle SPC (Server Playback Context) and CKC (Content Key Context) exchange
4. **AVContentKeySession:** Use modern content key session APIs

```swift
class FairPlayManager: NSObject {
    private let contentKeySession = AVContentKeySession(keySystem: .fairPlayStreaming)
    
    func setupFairPlay() {
        contentKeySession.setDelegate(self, queue: DispatchQueue.main)
    }
}

extension FairPlayManager: AVContentKeySessionDelegate {
    func contentKeySession(_ session: AVContentKeySession, 
                          didProvide keyRequest: AVContentKeyRequest) {
        // Handle key request
        handleContentKeyRequest(keyRequest)
    }
}
```

### Q5: What security measures would you implement to prevent content piracy?
**Answer:**
- **Certificate Pinning:** Prevent man-in-the-middle attacks
- **Root/Jailbreak Detection:** Block access on compromised devices
- **Screen Recording Prevention:** Use `UIScreen.isCaptured` and disable playback
- **Watermarking:** Implement forensic watermarking for content tracking
- **Token-based Authentication:** Short-lived tokens for content access
- **HDCP Compliance:** Ensure proper digital content protection

## Performance & Optimization

### Q6: How do you optimize video playback performance and reduce battery consumption?
**Answer:**
- **Hardware Acceleration:** Ensure H.264/H.265 hardware decoding
- **Efficient Rendering:** Use `AVPlayerLayer` instead of custom rendering
- **Background Playback:** Implement proper background audio sessions
- **Network Optimization:** Minimize redundant network requests
- **Memory Management:** Properly release video resources when not needed
- **Picture-in-Picture:** Implement PiP for better user experience

```swift
// Battery optimization
player.automaticallyWaitsToMinimizeStalling = true
player.preventsDisplaySleepDuringVideoPlayback = true

// Background audio session
try AVAudioSession.sharedInstance().setCategory(.playback, mode: .moviePlayback)
```

### Q7: How would you implement efficient thumbnail generation and seeking?
**Answer:**
Use `AVAssetImageGenerator` for thumbnail generation with optimization:

```swift
class ThumbnailGenerator {
    func generateThumbnails(for asset: AVAsset, count: Int) -> [UIImage] {
        let generator = AVAssetImageGenerator(asset: asset)
        generator.appliesPreferredTrackTransform = true
        generator.maximumSize = CGSize(width: 150, height: 150)
        
        // Generate thumbnails at specific intervals
        let duration = asset.duration
        let interval = CMTimeGetSeconds(duration) / Double(count)
        
        var thumbnails: [UIImage] = []
        for i in 0..<count {
            let time = CMTime(seconds: Double(i) * interval, preferredTimescale: 600)
            if let cgImage = try? generator.copyCGImage(at: time, actualTime: nil) {
                thumbnails.append(UIImage(cgImage: cgImage))
            }
        }
        return thumbnails
    }
}
```

## Architecture & Design Patterns

### Q8: How would you architect a scalable OTT app with offline capabilities?
**Answer:**
Implement a layered architecture:

1. **Repository Pattern:** Abstract data sources (network, cache, offline)
2. **MVVM with Coordinators:** Separate UI logic and navigation
3. **Dependency Injection:** Use protocols for testability
4. **Core Data/Realm:** Local storage for offline content metadata
5. **Background Downloads:** `AVAssetDownloadTask` for content downloading

```swift
protocol VideoRepository {
    func fetchVideo(id: String) -> AnyPublisher<Video, Error>
    func downloadVideo(id: String) -> AnyPublisher<DownloadProgress, Error>
    func getOfflineVideos() -> [Video]
}

class DefaultVideoRepository: VideoRepository {
    private let networkService: NetworkService
    private let cacheService: CacheService
    private let downloadManager: DownloadManager
    
    // Implementation details...
}
```

### Q9: How do you handle state management in a complex OTT app?
**Answer:**
Use a combination of approaches:
- **Redux/TCA:** For global app state
- **Combine:** For reactive data flows
- **AVPlayer Observation:** For playback state
- **UserDefaults/Keychain:** For user preferences and credentials

```swift
// Example using Combine
class PlaybackViewModel: ObservableObject {
    @Published var playbackState: PlaybackState = .stopped
    @Published var currentTime: CMTime = .zero
    @Published var duration: CMTime = .zero
    
    private var cancellables = Set<AnyCancellable>()
    
    func observePlayer(_ player: AVPlayer) {
        player.publisher(for: \.timeControlStatus)
            .map { status in
                switch status {
                case .playing: return .playing
                case .paused: return .paused
                case .waitingToPlayAtSpecifiedRate: return .buffering
                @unknown default: return .stopped
                }
            }
            .assign(to: &$playbackState)
    }
}
```

## Analytics & Monitoring

### Q10: How would you implement comprehensive video analytics?
**Answer:**
Implement analytics tracking for:
- **Playback Events:** Play, pause, seek, completion
- **Quality Metrics:** Bitrate changes, buffering events, errors
- **User Engagement:** Watch time, drop-off points, replay rates
- **Performance Metrics:** Startup time, buffering ratio, error rates

```swift
class VideoAnalytics {
    private let analyticsService: AnalyticsService
    
    func trackPlaybackStart(videoId: String, quality: String) {
        let event = AnalyticsEvent(
            name: "video_playback_start",
            parameters: [
                "video_id": videoId,
                "quality": quality,
                "timestamp": Date().timeIntervalSince1970
            ]
        )
        analyticsService.track(event)
    }
    
    func trackBufferingEvent(duration: TimeInterval) {
        // Track buffering metrics
    }
}
```

## Testing & Quality Assurance

### Q11: How do you test video playback functionality?
**Answer:**
Implement comprehensive testing strategy:
- **Unit Tests:** Test business logic and data models
- **Integration Tests:** Test network and playback integration
- **UI Tests:** Automated playback scenarios
- **Manual Testing:** Cross-device compatibility
- **Performance Testing:** Memory leaks, battery usage

```swift
// Example unit test
class VideoPlayerTests: XCTestCase {
    func testPlaybackStateTransitions() {
        let player = MockVideoPlayer()
        let viewModel = PlaybackViewModel(player: player)
        
        // Test state transitions
        XCTAssertEqual(viewModel.playbackState, .stopped)
        
        player.simulatePlay()
        XCTAssertEqual(viewModel.playbackState, .playing)
    }
}
```

## Infrastructure & DevOps

### Q12: How would you implement CI/CD for an OTT app?
**Answer:**
- **Automated Testing:** Run unit and UI tests on every commit
- **Code Signing:** Automated certificate management
- **Beta Distribution:** TestFlight integration for internal testing
- **Monitoring:** Crash reporting and performance monitoring
- **Feature Flags:** Remote configuration for A/B testing

### Q13: How do you handle different device capabilities and iOS versions?
**Answer:**
- **Capability Checking:** Check for hardware decoding support
- **iOS Version Compatibility:** Use `@available` attributes
- **Device-Specific Optimizations:** Different configurations for iPhone/iPad/Apple TV
- **Graceful Degradation:** Fallback options for older devices

```swift
if #available(iOS 14.0, *) {
    // Use modern APIs
    player.audiovisualBackgroundPlaybackPolicy = .continuesIfPossible
} else {
    // Fallback implementation
}

// Check device capabilities
if AVPlayer.availableHDRModes.contains(.hlg) {
    // Enable HDR playback
}
```

## Advanced Topics

### Q14: How would you implement Picture-in-Picture (PiP) functionality?
**Answer:**
```swift
import AVKit

class PiPManager: NSObject {
    private var pipController: AVPictureInPictureController?
    
    func setupPiP(with playerLayer: AVPlayerLayer) {
        guard AVPictureInPictureController.isPictureInPictureSupported() else { return }
        
        pipController = AVPictureInPictureController(playerLayer: playerLayer)
        pipController?.delegate = self
    }
    
    func startPiP() {
        pipController?.startPictureInPicture()
    }
}

extension PiPManager: AVPictureInPictureControllerDelegate {
    func pictureInPictureControllerWillStartPictureInPicture(_ pictureInPictureController: AVPictureInPictureController) {
        // Handle PiP start
    }
}
```

### Q15: How do you implement custom video controls and UI?
**Answer:**
Create custom controls while maintaining accessibility:
- **Custom Player View:** Overlay controls on `AVPlayerLayer`
- **Gesture Recognition:** Tap, swipe, pinch gestures
- **Accessibility:** VoiceOver support for controls
- **Auto-hide Logic:** Smart control visibility management
- **Responsive Design:** Adapt to different screen sizes

This comprehensive guide covers the essential areas for an OTT iOS senior developer interview. Each topic includes practical implementation details and code examples that demonstrate real-world experience with streaming applications.
