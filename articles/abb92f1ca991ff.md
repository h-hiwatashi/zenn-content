---
title: "video_playerをHooksで実装してみた"
emoji: "🐮"
type: "tech"
topics:
  - "flutter"
published: true
published_at: "2025-01-13 23:44"
---

# この記事について
Flutter Widget of the Weekでvideo_playerが取り上げられていて、videoの実装をしたことがなかったため勉強のためにhooksで実装してみました！
https://youtu.be/Jxw6FaA0j3I?si=YOeZ3pCRibOhkKIK

## cookbook
https://docs.flutter.dev/cookbook/plugins/play-video

# コード
```dart
import 'package:flutter/material.dart';
import 'package:flutter_hooks/flutter_hooks.dart';
import 'package:video_player/video_player.dart';

class VideoPlayerView extends HookWidget {
  const VideoPlayerView({super.key});

  @override
  Widget build(BuildContext context) {
    final controller = useMemoized(() => VideoPlayerController.networkUrl(Uri.parse(
        'https://flutter.github.io/assets-for-api-docs/assets/videos/butterfly.mp4')));
    final initialized = useState(false);
    final isPlaying = useState(false);

    useEffect(() {
      controller.initialize().then((_) {
        initialized.value = true;
        isPlaying.value = controller.value.isPlaying;
      });
      controller.addListener(() {
        isPlaying.value = controller.value.isPlaying;
      });

      return controller.dispose;
    }, [controller]);

    return Scaffold(
      appBar: AppBar(
        title: Text('Video Player View'),
      ),
      body: Center(
        child: controller.value.isInitialized
            ? AspectRatio(
                aspectRatio: controller.value.aspectRatio,
                child: VideoPlayer(controller),
              )
            : CircularProgressIndicator(),
      ),
      floatingActionButton: FloatingActionButton(
        onPressed: () {
          controller.value.isPlaying ? controller.pause() : controller.play();
        },
        child: Icon(
          isPlaying.value ? Icons.pause : Icons.play_arrow,
        ),
      ),
    );
  }
}

```

いい感じに動画再生してくれます。
![](https://storage.googleapis.com/zenn-user-upload/9b9fc4683468-20250113.png =300x)

# まとめ
簡単に動画再生機能が作れました。
hooksの練習がてら色々なwidgetを作ってみようと思います。