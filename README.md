# koryo-wait.github.io.io
<!DOCTYPE html>
<html lang="ja">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width,initial-scale=1">
  <title>はじめてのサイト</title>
  <style>
    /* 簡単な見た目調整（任意） */
    body { font-family: system-ui, -apple-system, "Hiragino Kaku Gothic ProN", "Noto Sans JP", "メイリオ", sans-serif; padding: 1rem; }
    h1 { margin-bottom: 0.5rem; }
    #wait { font-size: 1.25rem; font-weight: 600; }
  </style>
</head>
<body>
  <h1>現在の待ち時間</h1>
  <!-- aria-live で更新を支援技術に通知 -->
  <p id="wait" aria-live="polite">読み込み中…</p>

  <script>
    // 初期の残り分（任意で変更）
    let minutes = 3;

    const el = document.getElementById("wait");
    let timerId = null;

    function updateDisplay() {
      if (minutes > 0) {
        // 現在の残り分を表示してからカウントダウン
        el.textContent = minutes + "分待ち";
        minutes--;
      } else {
        // 0分以下になったら案内可能にしてタイマーを停止
        el.textContent = "ご案内できます";
        if (timerId) {
          clearInterval(timerId);
          timerId = null;
        }
      }
    }

    // ページ読み込み時に即座に表示を初期化
    updateDisplay();

    // 残り分がある場合は1分ごとに更新（60000ms）
    if (minutes > 0) {
      timerId = setInterval(updateDisplay, 60000);
    }
  </script>
</body>
</html>
