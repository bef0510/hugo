+++
date = '2024-12-06T15:31:24+08:00'
draft = true
title = '使用 Web Speech API'
tags = ['Html', 'WebSpeechAPI']
categories = ['Html']
+++

## 使用 **Web Speech API**

#### 1. **html**
```
<div>
	<input id="text" type="text" class="ai-inputtext ai-input-text" />
	<button type="button" class="ai-button ai-send-button ml-2" onclick="onStartSpeechToTxt()">
		<span id="record" class="ai-send-button-label">
			<svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-record2-fill" viewBox="0 0 16 16">
				<path d="M10 8a2 2 0 1 1-4 0 2 2 0 0 1 4 0"/>
				<path d="M8 13A5 5 0 1 0 8 3a5 5 0 0 0 0 10m0-2a3 3 0 1 1 0-6 3 3 0 0 1 0 6"/>
			</svg>
		</span>
		<span id="pause" class="ai-send-button-label" style="display: none">
			<svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-record2-fill" viewBox="0 0 16 16">
				<path d="M5.5 3.5A1.5 1.5 0 0 1 7 5v6a1.5 1.5 0 0 1-3 0V5a1.5 1.5 0 0 1 1.5-1.5m5 0A1.5 1.5 0 0 1 12 5v6a1.5 1.5 0 0 1-3 0V5a1.5 1.5 0 0 1 1.5-1.5"/>
			</svg>
		</span>
	</button>
</div>
```

#### 2. **js**
```
$(function() {
	// 初始設定
	state = { isGoing: false };
	window.SpeechRecognition = window.SpeechRecognition || window.webkitSpeechRecognition;
	recognition = new window.SpeechRecognition();

	// 設定語言為中文
	recognition.lang = 'zh-TW';

	// 設定為連續模式
	recognition.continuous = true;

	// 設定為顯示中間結果
	recognition.interimResults = true;

	// event current voice reco word
	recognition.onresult = function(event) {
		let result = Array.from(event.results)
			.map(result => result[0])
			.map(result => result.transcript)
			.join("");

		$("#text").val(result);
	};
});

function onStartSpeechToTxt() {
	let record = $("#record");
	let pause = $("#pause");

	if(state.isGoing) {
		record.show();
		pause.hide();
		
		// 結束語音識別
		recognition.stop();
		state.isGoing = false;
	} else {
		record.hide();
		pause.show();
		
		// 開始語音識別
		recognition.start();
		state.isGoing = true;
	}
}
```

#### 3. **css**
```
.ai-button {
    color: #fff;
    background: #3B82F6;
    border: 1px solid #3B82F6;
    padding: .75rem 1.25rem;
    border-radius: 6px;
}

.ai-button:enabled:hover {
    background: #2563eb;
    color: #fff;
    border-color: #2563eb;
}

.ai-send-button {
    font-size: 1.5rem;
    border-radius: 6px;
    color: #fff;
    background: #3B82F6;
    border: 1px solid #3B82F6;
}

input, button, select, textarea {
    font-family: inherit;
    font-size: inherit;
    line-height: inherit;
}

.ai-input-text {
    width: 42vh;
    margin-right: 10px;
}

.ai-inputtext {
    color: #495057;
    background: #ffffff;
    padding: .75rem;
    border: 1px solid #ced4da;
    transition: background-color .2s, color .2s, border-color .2s, box-shadow .2s;
    -webkit-appearance: none;
    appearance: none;
    border-radius: 6px;
}
```

#### 4. 網頁點擊錄音
![](/images/003_webSpeechAPI/01.png)

#### 5. 網頁點擊錄音
![](/images/003_webSpeechAPI/02.png)
![](/images/003_webSpeechAPI/03.png)

## 參考
[SpeechRecognition](https://developer.mozilla.org/en-US/docs/Web/API/SpeechRecognition "")