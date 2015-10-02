# onlyNumber
input[type=text] only input Number


# Input 输入框 只允许输入数字

// 校验 负号只能在第一位

// 校验 负号如果有只能有一位

// 校验 小数点如果有只能有一位

// 校验 小数点在第一位时自动补零

// 校验 负号后直接跟小数点 "-." ==> "-0." 

# 调用方式

  将事件直接委托在父级上
  
    var oBody = $("body");
    oBody.onlyNumber({
        className: '.plNumber',
        isDecimal: true,
        isMinus: false
    });
