+++
title = 'View Transitions'
date = 2024-12-19T20:56:34+05:30
draft = false
+++


Works on Chrome based browsers as of 19 Dec 2024

```html
<!doctype html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <title>Document</title>
    </head>
    <style>
        .card {
            view-transition-name: card;
            width: 60px;
            height: 80px;
            background: white;
            border: 0.5px solid #ccc;
            box-shadow: 0 0 1px black;
            border-radius: 5px;
        }

        .card-two {
            translate: 200px 200px;
            scale: 3;
            background: red;
        }
    </style>
    <body>
        <button class="card card-one" onclick="toggleFunc()">A</button>
        <button
            class="card card-two"
            onclick="toggleFunc()"
            style="display: none"
        >
            Q
        </button>
    </body>
    <script>
        var toggleFunc;
        window.onload = () => {
            var toggle = false;
            var card = document.getElementsByClassName("card")[0];
            toggleFunc = () => {
                document.startViewTransition(() => {
                    toggle = !toggle;
                    if (!toggle) {
                        document.getElementsByClassName(
                            "card-one",
                        )[0].style.display = "block";
                        document.getElementsByClassName(
                            "card-two",
                        )[0].style.display = "none";
                    } else {
                        document.getElementsByClassName(
                            "card-one",
                        )[0].style.display = "none";
                        document.getElementsByClassName(
                            "card-two",
                        )[0].style.display = "block";
                    }
                });
            };
        };
    </script>
</html>
```

{{< youtube "jnYjIDKyKHw" >}}


# References

1. [View Transitions Are More Powerful Than You Think - YouTube](https://www.youtube.com/watch?v=jnYjIDKyKHw&ab_channel=Syntax)
