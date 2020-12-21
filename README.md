### Notas sobre o curso de Node

## CSS Architecture

# BEM 
B = Block: independent, reusable part of our design (like the large hero section our features in features section or testmonials in testmonials section)
E = Element: belongs to a block, cannot be used outside that block (like a title/subtitle)
M = Modifier: class that can be used on block or element. Indicate change on default state

Important concepts:
- CSS selectors should target elements directly, instead of relying on type selectors, descendent selectores and the cascade
- Because we are limiting cascade, we are gree to move blocks around and reuse them throughout the page
- Blocks can be nested inside other blocks
- Idea is to identify patterns and then create single-responsability blocks that can be reused (no need to code patterns more than once)
- Makes the relationship between HTML and CSS clear (enhance maintainability)

Why extra classes with presentational names is not making HTML less semantic?

*Note: what is semantic HTML?

- Classes cannot be unsemantic
- Content-layer semantics are already served by HTML elements
- Class names impart little or no useful semantics to machines or human visitors
- THe primary purpose of a class name is to be a hook for CSS and Javascript
- Class names should communicate useful information to developers

# Traditional Nesting

Conceptual Organization
On the 'large hero' example, the large hero is the block and examples of elements would be title and subtitle.
So class names become, for example 'large-hero__title'.
In traditional CSS design, nesting would be  

```sh
.large-hero{
    position: relative;
}

.large-hero__text-content{
    position: absolute;
    top: 50%;
    transform: translateY(-50%);
    left: 0;
    width: 100%;
    text-align: center;
}

.large-hero__title {
    font-weight: 300;
    color: #2f5572;
    font-size: 4.8rem;
}

.large-hero__subtitle {
    font-weight: 300;
    color: #2f5572;
    font-size: 2.9rem;
}
```
To

```sh
.large-hero{
    position: relative;

    .large-hero__text-content{
        position: absolute;
        top: 50%;
        transform: translateY(-50%);
        left: 0;
        width: 100%;
        text-align: center;
    }      

    .large-hero__title {
        font-weight: 300;
        color: #2f5572;
        font-size: 4.8rem;
    }   

    .large-hero__subtitle {
        font-weight: 300;
        color: #2f5572;
        font-size: 2.9rem;
    }

}
```

But in compiling, this would lead to descendent selectors:

```sh
.large-hero{
    position: relative;
}

.large-hero .large-hero__text-content{
    position: absolute;
    top: 50%;
    transform: translateY(-50%);
    left: 0;
    width: 100%;
    text-align: center;
}  

...
```

# PostCSS Nesting Feature

Instead, we can use PostCSS nesting feature as follow:
```sh
.large-hero{
    position: relative;

    &__text-content{
        position: absolute;
        top: 50%;
        transform: translateY(-50%);
        left: 0;
        width: 100%;
        text-align: center;
    }

    &__title {
        font-weight: 300;
        color: #2f5572;
        font-size: 4.8rem;
    }

    &__subtitle {
        font-weight: 300;
        color: #2f5572;
        font-size: 2.9rem;
    }
}
```

That will lead to:

```sh
.large-hero{
    position: relative;
}

.large-hero__text-content{
    position: absolute;
    top: 50%;
    transform: translateY(-50%);
    left: 0;
    width: 100%;
    text-align: center;
}

.large-hero__title {
    font-weight: 300;
    color: #2f5572;
    font-size: 4.8rem;
}

.large-hero__subtitle {
    font-weight: 300;
    color: #2f5572;
    font-size: 2.9rem;
}
```
