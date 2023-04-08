在 JavaScript 中我们已经学过 DOM 相关的操作了，对于 DOM 创建的流程我们简单回顾一下。整个创建流程可分为以下几个步骤：

- 创建元素节点。
- 给元素添加属性。
- 在标签中添加一些文本。
- 把该元素放入整个文档中。

对于 JavaScript 的繁琐步骤，我们的 jQuery 有自己的优化措施。通过使用 `$()` 来创建元素节点，常见的创建有以下三种。

1. 直接创建元素节点。
2. 创建带有文本的元素节点。
3. 创建带有属性的元素节点。

```
$('.card-body-option-favorite img').on('click', function() {
        if($(this).attr('src') === './images/hollow.svg') {
          $(this).attr('src', './images/solid.svg')
          $('#toast__container').css("display", "block")
          setTimeout(() => {
            $('#toast__container').fadeOut(1000);
          }, 2000);
          $('.toast__close').on('click', function() {
            $('#toast__container').fadeOut()
          })
        } else {
          $(this).attr('src', './images/hollow.svg')
        }
      })
```

```
    // TODO：待补充代码
    //toast__container
    //card-body-option-favorite
    //container
    let hearts = [...document.querySelectorAll(".card-body-option-favorite>img")];
    let box = document.getElementById('toast__container');
    hearts.forEach(element => {
      console.log();
      element.addEventListener('click', function () {
        if (element.getAttribute('src') == './images/hollow.svg') {
          element.setAttribute('src', './images/solid.svg');
          box.style.display = 'block';
          document.querySelector('.toast__close>img').addEventListener('click',function () {
            console.log("被点击");
            box.style.display = 'none';
          })
          setTimeout(() => {
            box.style.display = 'none';
          }, 2000);
        } else {
          element.setAttribute('src', './images/hollow.svg');
        }

      })
    });
```

