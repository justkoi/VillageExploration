# 마을탐험

프로젝트 소개 : 마을탐험은 여러 마을을 오가면서 다양한 사건을 조사해 나가는 퀘스트 수행 형식의 어드벤처 게임입니다.

사용 기술 : Flash Action Script 2.0, Macromedia Flash MX 2004

담당 역할 : 게임 개발 전체

개발기간 : 2007년 8월 ~  2007년 9월

핵심 기술 / 알고리즘 : 플레이어 이동, 프레임 이동, 퀘스트 수행

핵심코드 : 

```Action Script 2.0
플레이어 무비클립 액션
onClipEvent (load) {
	var spd = 8;
}
onClipEvent (enterFrame) {
	if (Key.isDown(Key.RIGHT)) {
		this.gotoAndPlay(3);
		this._x += spd;
	}
}
onClipEvent (enterFrame) {
	if (Key.isDown(Key.LEFT)) {
		this.gotoAndPlay(1);
		this._x -= spd;
	}
}
onClipEvent (enterFrame) {
	if (Key.isDown(Key.DOWN)) {
		this.gotoAndPlay(4);
		this._y += spd;
	}
}
onClipEvent (enterFrame) {
	if (Key.isDown(Key.UP)) {
		this.gotoAndPlay(2);
		this._y -= spd;
	}
}
onClipEvent (enterFrame) {
	if (this._x>550-this._width || this._x<0+this._width) {
		this._x = 353;
	}
}
onClipEvent (enterFrame) {
	if (this._y>303.9-this._height || this._y<0+this._height) {
		this._y = 204.3;
	}
}
의의 : 변수의 개념 및 조건절의 이해. (캐릭터 이동속도 spd 및 화면밖으로 나가지 못하게 처리)
```

```
포탈 액션
onClipEvent (enterFrame) {
	if (_root.hr.hitTest(this)) {
		_root.text1._visible = true;
	} else {
		_root.text1._visible = false;
	}
}
onClipEvent (keyDown) {
	if (_root.hr.hitTest(this) && Key.isDown(Key.SPACE)) {
		_root.hr._x = 60;
		_root.gotoAndPlay(4);
	}
}
의의 : 무비클립과 무비클립 사이의 히트박스에 따른 충돌처리 이해 (hitTest 메서드). 
충돌하는중에(and) 스페이스가 눌린 경우 프레임(씬) 이동 처리. (조건절 and 및 or 연산자 이해)
```

```
메인 프레임. 세이브 & 로드.
var money:Number = 0;
var h2:Number = 100;
var key:Number = 1;
var qstn = 1;


_global.saveGame = function() {
	saveName = "123456";
	myLSO = SharedObject.getLocal(saveName);
	if (myLSO.data.myObj == undefined) {
		trace("게임 저장");
	} else {
		trace("이전 게임 저장");
	}
	myObj = {};
	myObj.objArray = new Array();
	myObj.objArray[0] = money;
	myObj.objArray[1] = qstn;
	myObj.objArray[2] = h2;
	myObj.objArray[3] = key;
	myLSO.data.myObj = myObj;
};
_global.loadGame = function() {
	var _local1 = _root;
	loadName = "123456";
	myLSO = SharedObject.getLocal(loadName);
	if (myLSO.data.myObj == undefined) {
	} else {
		money = myLSO.data.myObj.objArray[0];
		qstn = myLSO.data.myObj.objArray[1];
		h2 = myLSO.data.myObj.objArray[2];
		key = myLSO.data.myObj.objArray[2];
	}
};
var h:Number = 0;
의의 : 전역변수의 이해 (다른 하위 무비클립의 action에서 전역변수(퀘스트)값을 수정하였으며 그 값에 의존하여 작동하도록 퀘스트 시스템을 구현함)
```

최초 업로드 홈페이지 : https://cafe.naver.com/shiftouch/187504

플레이 영상 : https://youtu.be/YOkyj1Wgd54

프로젝트 주소 : https://github.com/justkoi/VillageExploration

