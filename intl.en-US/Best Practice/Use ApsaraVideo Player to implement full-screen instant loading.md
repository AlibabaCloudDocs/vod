# Use ApsaraVideo Player to implement full-screen instant loading

ApsaraVideo Player allows you to implement full-screen instant loading by using the following three methods: the first frame as the thumbnail, video preload, and play-and-cache. You can use these methods to shorten the average startup loading time to about 300 milliseconds in a Wi-Fi environment.

## First frame as the thumbnail

-   Before a video is played, its thumbnail is displayed. If you use the first frame as the thumbnail, users are convinced that the playback starts when they see the thumbnail. It seems that the video is instantly played.
-   Only thumbnails are requested when a user scrolls through the video playlist in a quick manner.
-   When a user scrolls to half of the next video, the downloaded video thumbnail is displayed.

## Video preload

Create multiple players

ApsaraVideo Player does not support progressive download. To use the preload feature, you must create multiple players.

The AliListPlayer operation is added to ApsaraVideo Player SDK V4.5.0 and later. You can use the preload feature by calling this operation. For more information, see [Implementation](/intl.en-US/New Player SDK/ApsaraVideo Player SDK for Android/Implementation.md).

-   You can use the short video list player based on the video ID and Security Token Service \(STS\) token or based on the video URL.
-   You cannot use the short video list player to play videos in the M3U8 format. You can create multiple AliPlayer objects to implement the preload feature as needed.

## Play-and-cache

You can use the play-and-cache feature to cache a video to your on-premises machine when the video is being played. When you play the video again, ApsaraVideo Player uses the cached file for playback without requesting for the video online.

You can set the download path, maximum download size, and maximum allowed download duration for a single video. The unit of the maximum download size is MB and that of the maximum allowed download duration is seconds.

```
 // The sample code for Android.
 // Set the cache directory after you create a player class and before you call the prepare method.
  String sdDir = Environment.getExternalStorageDirectory().getAbsolutePath() + "/test_save_cache";   aliyunVodPlayer.setPlayingCache(true, sdDir, 60 * 60 /*The maximum duration of a single video, in seconds. */, 300 /* The total size of files in the cache directory, in MB.*/);
// For example, if the maxSize parameter is set to 500 MB and the size of files in the cache directory exceeds 500 MB, the system overwrites the earliest cached files. If the maxDuration parameter is set to 300 seconds and the duration of a video exceeds 300 seconds, the excess part of the video is not cached.

// The sample code for iOS.
// Set the cache directory
NSArray *pathArray = NSSearchPathForDirectoriesInDomains(NSDocumentDirectory, NSUserDomainMask, YES);
NSString *docDir = [pathArray objectAtIndex:0];
after you create a player class and before you call the prepare method. // For example, if the maxSize parameter is set to 500 MB and the size of files in the cache directory exceeds 500 MB, the system overwrites the earliest cached files. If the maxDuration parameter is set to 300 seconds and the duration of a video exceeds 300 seconds, the excess part of the video is not cached.
[self.aliPlayer setPlayingCache:YES saveDir:docDir maxSize:500 maxDuration:300];
```

**Note:**

-   The play-and-cache feature only caches videos that are fully played. If you perform seeking during playback, the video cannot be cached. This feature applies to loop playback of short videos.
-   The play-and-cache feature must be enabled before the prepare method is called.

## Enable refresh and prefetch

Log on to the ApsaraVideo VOD console and click Refresh and Push. Set the Operation parameter to Push and enter the URL of the video that you want to prefetch.

![Prefetch](../images/p184118.jpg)

**Note:** The refresh and prefetch feature charges you a fee. You can prefetch videos to Alibaba Cloud Content Delivery Network \(CDN\) nodes based on video popularity.

