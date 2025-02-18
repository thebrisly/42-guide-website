---
description: A tool to facilitate complex if ... else if statements.
---

# 🔄 Switch statement

The `switch` and `case` statements cannot be used most of the time since they are not in the `Norm`.

It could be useful in some exams, and you can use it there since there is no `Norm` during the exams.

### Switch statement

The `switch` and `case` statements help control complex conditional and branching operation.

### Examples

I'll take as example one of the exercises of the `exam rank 02 - level 2`, the [`do_op`](../exams/exam-rank-02/level-2/do_op.md) one, go read the subject there, then come back here.

I'll first write it using if and else if statements, then I'll write the exact same thing using the `switch` statement.

#### If ... else if

<pre class="language-c" data-overflow="wrap" data-line-numbers><code class="lang-c">if (av[2][0] == '+')
    printf("%d", atoi(av[1]) + atoi(av[3]));
else if (av[2][0] == '-')
    printf("%d", atoi(av[1]) - atoi(av[3]));
else if (av[2][0] == '*')
<strong>    printf("%d", atoi(av[1]) * atoi(av[3]));
</strong><strong>else if (av[2][0] == '/')
</strong><strong>    printf("%d", atoi(av[1]) / atoi(av[3]));
</strong><strong>else if (av[2][0] == '%')
</strong><strong>    printf("%d", atoi(av[1]) % atoi(av[3]));
</strong></code></pre>

#### Switch

{% code overflow="wrap" lineNumbers="true" %}
```c
swtich (av[2][0])
{
    case '+':
        printf("%d", atoi(av[1]) + atoi(av[3]));
        break;
    case '-':
        printf("%d", atoi(av[1]) - atoi(av[3]));
        break;
    case '*':
        printf("%d", atoi(av[1]) * atoi(av[3]));
        break;
    case '/':
        printf("%d", atoi(av[1]) / atoi(av[3]));
        break;
    case '%':
        printf("%d", atoi(av[1]) % atoi(av[3]));
        break;
}
```
{% endcode %}

As you can see, both codes are pretty similar, but I personally think that the `switch` statement is clearer and easier to write.

The switch statement takes a bit more place but could be useful in some cases.

You can find more details about it [here](https://www.w3schools.com/c/c_switch.php).
