---
layout: post
title:  "分享我的几个GitHub数学类开源项目"
date:   2016-08-01 16:00:00 +0800
categories: code
---

之前在开发[「分形的奥秘」][appstore-link]时积攒了一些与数学关系密切的Swift代码片段，有的非常有趣，有的还有实际使用价值。因此我把它们单独整理了出来，全部用Xcode Playground呈现。现在已经将3个项目放到GitHub上了，欢迎开发者和爱好者参观。

# 1. 复数运算 － swift-complex-number

[➞ 前往这个Repo：https://github.com/gongzhang/swift-complex-number][swift-complex-number]

复数(Complex Number)是什么？复数就是实数＋虚数(imaginary number)。虚数是什么？虚数就是“-1”开根号。虚数这个概念好像高中数学里面就有，不过高考之后应该就没什么印象了，毕竟概念太抽象，不学相关专业的话完全不能领会这个“凭空”制造的概念有什么实际用途（虽然极其有用）。

{% include retina-image.html path="images/github/exam-math.png" %}

> *[这高考题][exam]你们还有多少印象？*

虚数（或复数）在编程语言中很容易实现，用两个浮点数分量代表“实部”和“虚部”就可以了。不过有趣的是，利用Swift的自定义运算符特性，可以在代码中模仿出特有的数学专业记法。像这样：

```swift
print(𝒊 ^ 2 == -1) // true
```

注意上面的虚数单位“𝒊”是个Unicode字符，而非小写英文字母“i”。代码里的“𝒊”是预先定义好的虚数单位，就像数学课本里的“𝒊”一样。

利用Swift的运算符重载特性，可以实现复数的基本运算：

```swift
let c1 = 3 + 2 * 𝒊  // 3 + 2𝒊, same with Complex(3, 2)
let c2 = 1 - 4 * 𝒊  // 1 - 4𝒊, same with Complex(1, -4)

print(c1 * c2 - (2 - 4 * 𝒊)) // 9 - 6𝒊
```

甚至可以用Unicode创建新的运算符，来实现复数的角度记法：

```swift
let c3 = r ∠ φ // r * (cos(φ) + sin(φ) * 𝒊)
```

关于Swift自定义运算符方面的应用，[@Mattt][mattt]大神还专门开过一个在Swift中实现常见数学记法的项目，项目名叫[Euler][euler]，强烈推荐围观。

当然，这些Unicode运算符不会给实际开发带来多少好处，而且输入很麻烦。不过此类项目的目的也并不在于效率，而在于美（qiang）感（po）。

# 2. 绘制Julia集合分形 － julia-set-playground

[➞ 前往这个Repo：https://github.com/gongzhang/julia-set-playground][julia-set-playground]

[@Matrix67][matrix67]大神的数学博客上有多篇文章都是有关分形主题的，可以到[这里][matrix67-fractal]阅读。我之前也是受他启发才开发了[「分形的奥秘」][appstore-link]这个app。现在我把绘制Julia集合分形的Swift代码共享出来，有兴趣的朋友可以用Xcode Playground一探究竟。

{% include retina-image.html path="images/github/juliaset.png" %}

> *Xcode Playground中的运行效果*

分形图像样子虽复杂，但其实只需要一个简单迭代就可以生成，原理非常简单。经典的*逃逸时间*算法，图像是“pixel-by-pixel”依次计算每一个像素生成的。代码里面我用*GCD(Grand Central Dispatch)*稍挖掘了一下多核CPU的并行能力，在我的MacBook Pro上执行比移动设备快很多。

当然，此类计算任务还是最适合交给GPU来做。不过就算是GPU，直接在iPhone和iPad上全屏渲染也是比较卡的，最新的机型也是，毕竟计算量在那里摆着。不信可以拿OpenGL或Metal试试ᶘ ᵒᴥᵒᶅ。[「分形的奥秘」][appstore-link]里面我用了好几种优化手段才做到主流iOS设备流畅渲染，以后专门写篇文章好了。

# 3. 图像傅立叶变换 － fft2d-swift-playground

[➞ 前往这个Repo：https://github.com/gongzhang/fft2d-swift-playground][fft2d-swift-playground]

这个Repo其实不算是我原创的，我只是将[另一个][js-fft]JavaScript实现的图像FFT代码用Swift翻写了一遍，可以在Playground里玩、可读性更好一些罢了。

关于傅立叶变换，确实不太容易从直观角度理解，不过仍然有非常好的文章把傅立叶变换的直观意义讲解地很透彻，比如[这篇][fourier-zhihu]。写这个Repo纯粹是自娱自乐，复习一下傅立叶变换，没有什么直接目的。之后可以拿来分析图像的频率信息分布，评估图像的视觉效果，应该用得上。

{% include retina-image.html path="images/github/fft.png" %}

> *“图文并茂”*

实现傅立叶变换（二维快速离散傅立叶变换）的时候，当中也是有用到复数概念的。因此直接用上了前面的复数运算Repo的代码，利用率高吧？

# Recap

Swift和Playground真的极其适合展示程序片段和相关概念。期待今年9月苹果发布Xcode 8、Swift 3，还有iPad版的Swift Playground，希望它们变得更快更稳定。到时给你们展示更多好玩的代码。

[appstore-link]: https://itunes.apple.com/app/id1086527481
[swift-complex-number]: https://github.com/gongzhang/swift-complex-number
[exam]: http://wenku.baidu.com/link?url=RcsY3-YrIU5ENgcniZlQu_kcRfPBhO_1V1P71BS-JuSTR6CAcjiniVqZIpFj6uU0CPlm5gXCtidJMvhy14g1PGWYQWPYN-A9dpvlNqbehY_
[mattt]: https://github.com/mattt
[euler]: https://github.com/mattt/Euler
[julia-set-playground]: https://github.com/gongzhang/julia-set-playground
[matrix67]: http://www.matrix67.com
[matrix67-fractal]: http://www.matrix67.com/blog/archives/tag/分形
[fft2d-swift-playground]: https://github.com/gongzhang/fft2d-swift-playground
[js-fft]: https://github.com/turbomaze/JS-Fourier-Image-Analysis
[fourier-zhihu]: http://daily.zhihu.com/story/3939307