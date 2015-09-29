// 只能输入数字
// 校验 负号只能在第一位
// 校验 负号如果有只能有一位
// 校验 小数点如果有只能有一位
// 校验 小数点在第一位时自动补零
(function (factory) {
	if (typeof define === 'function' && define.amd) {
		define(['jquery'], factory);
	} else if (typeof exports === 'object') {
		factory(require('jquery'));
	} else {
		factory(jQuery);
	}
}(function ($) {

	// 只允许输入数字
	function onlyNumber(ev) {
		var code = ev.keyCode || ev.which;
		if((ev.ctrlKey && code == 97) || (ev.ctrlKey && code == 65)){  // Ctrl+A
			return true;
		}else if((ev.ctrlKey && code == 120) || (ev.ctrlKey && code == 88)){ // Ctrl+X
			return true;
		}else if((ev.ctrlKey && code == 99) || (ev.ctrlKey && code == 67)){ // Ctrl+C
			return true;
		}else if((ev.ctrlKey && code == 122) || (ev.ctrlKey && code == 90)){ // Ctrl+Z 
			return true;
		}else if((ev.ctrlKey && code == 118) || (ev.ctrlKey && code == 86) || (ev.shiftKey && code == 45)){ // Ctrl+V, Shift+Ins
			return true;
		}else if( (code >= 48 && code <= 57) ) { // number (keypress no smallKey)
	        return true;
		}else if( code == 8 || code == 9 || code == 37 || code == 39 ){ //backspace, tab, left, right
			return true;
		}else if( code == 13 ){ // enter
			return true;
		}else if( code == 46 || code == 45 ){ // del(.), minus(-)
			return true;
		}else{
			if (ev && ev.preventDefault)
	            ev.preventDefault(); //阻止默认浏览器动作(W3C)
			else
				window.event.returnValue = false; //IE中阻止函数器默认动作的方式 
			return false;
		}
	}
	// 校验
	function checkNumber (ev, isDecimal, isMinus) {
		var v = ev.target.value;
		v = v.replace(/\s/g,"");
		var dot = $.inArray('.', v.split(''));
		var minus = $.inArray('-', v.split(''));
		var length = v.length;
		var validChars = [0,1,2,3,4,5,6,7,8,9];
		if(v && length>0){
			if(isDecimal){
				if(dot === 0){
					v = '0' + v;
				}else{
					validChars.push('.');
					for(var i = length - 1; i >= 0; i--){
						var ch = v.charAt(i);
						var validChar = false;
						for(var j = 0; j < validChars.length; j++){
							if(ch == validChars[j]){
								validChar = true;
								break;
							}
						}
						if(!validChar || ch == " "){
							v = v.substring(0, i) + v.substring(i + 1);
						}
						var firstDecimal = $.inArray('.', v.split(''));
						if(firstDecimal > 0){
							for(var k = length - 1; k > firstDecimal; k--){
								var chch = v.charAt(k);
								if(chch == '.'){
									v = v.substring(0, k) + v.substring(k + 1);
								}
							}
						}
					}
				}
			}
			if(isMinus){
				if(minus === 0){
					v = '-' + v;
				}
			}
			if(!isDecimal && !isMinus){
				for(var i = length - 1; i >= 0; i--){
					var ch = v.charAt(i);
					var validChar = false;
					for(var j = 0; j < validChars.length; j++){
						if(ch == validChars[j]){
							validChar = true;
							break;
						}
					}
					if(!validChar || ch == " "){
						v = v.substring(0, i) + v.substring(i + 1);
					}
				}
			}
		}else{
			v = '';
		}
		ev.target.value = v;
	}

	$.fn.onlyNumber = function (options) {
		var defaults = {
			className: '',
			isDecimal: true,
			isMinus: true
		};
		var opts = $.extend({}, defaults, options);
		var oBody = $(this);
		oBody.delegate(opts.className, 'keypress', function (e) {
			onlyNumber(e);
		});
		oBody.delegate(opts.className, 'input', function (e) {
			checkNumber(e, opts.isDecimal, opts.isMinus);
		});
		return this;
	};

}));
