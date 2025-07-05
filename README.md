順番を保ったタスク実行を可能にする軽量なキューイングシステムを提供する Dart パッケージです。非同期タスクの順序付き実行とタスクの完了待機をサポートします。

## Features

- 非同期タスクの順序付き実行
- タスクの完了待機
- タスクキューの状態確認（isEmpty、isNotEmpty）
- すべてのタスクの完了待機（join()メソッド）
- 軽量で高性能な実装

## Getting started

`pubspec.yaml`にパッケージを追加してください：

```yaml
dependencies:
  task_queue: ^1.0.0
```

## Usage

### 基本的な使用例

```dart
import 'package:task_queue/task_queue.dart';

void main() async {
  final queue = TaskQueue();

  // タスクを順次実行
  final task1 = queue.queue(() async {
    await Future.delayed(Duration(milliseconds: 300));
    print('Task 1 completed');
    return 1;
  });

  final task2 = queue.queue(() async {
    await Future.delayed(Duration(milliseconds: 200));
    print('Task 2 completed');
    return 2;
  });

  // 結果を取得（順番に実行されるため、1, 2の順で完了）
  print('Result 1: ${await task1}'); // 1
  print('Result 2: ${await task2}'); // 2
}
```

### すべてのタスクの完了待機

```dart
void main() async {
  final queue = TaskQueue();

  // 複数のタスクを追加
  for (int i = 0; i < 5; i++) {
    queue.queue(() async {
      await Future.delayed(Duration(milliseconds: 100));
      print('Task $i completed');
    });
  }

  // すべてのタスクが完了するまで待機
  await queue.join();
  print('All tasks completed');
}
```

## Additional information

このパッケージは、非同期処理の順序制御が必要なアプリケーションに最適です。

- **リポジトリ**: https://github.com/eaglesakura/dart_task_queue
- **イシュー**: バグ報告や機能要求は[GitHub Issues](https://github.com/eaglesakura/dart_task_queue/issues)まで
- **貢献**: プルリクエストやイシューの報告を歓迎します
- **ライセンス**: 詳細は LICENSE ファイルを参照してください
