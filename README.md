# Lede 2024 Storytelling: Create SVG with D3

An 8-step guide to create a simple SVG graphic with D3.js

#### What to do before we start:
- Clone this repo to your computer (not sure how to? check it out [here](https://docs.github.com/en/repositories/creating-and-managing-repositories/cloning-a-repository)) or download the zip file to this repo using the green top button that says `CODE` 
- Navigate to the repo with terminal, and load a local server. 
    - You can use the following line if you use python. Once it says a local server is running, type in `localhost:8080` on your browser. You should see the content of the `index.html` page there!
        ```
        python3 -m http.server --cgi 8080
        ```
    - If you use VS Code, check out this plugin: [How to load changes spontanously on your local server with VS Code](https://www.freecodecamp.org/news/vscode-live-server-auto-refresh-browser/) 

## Preparation

1. Create a basic html page. If you don't know how, refers to Soma’s tutorial: [How to create and host a web pages on Github](https://jonathansoma.com/fancy-github/github-pages/). For this tutorial, you can use `index.html` as a starter. 


2. Add the d3 library to the page. For the purpose of this demo, we are loading the entire D3 library in one Javascript (js) file.  Add the following script to your HTML markup. 


    ```
    https://cdnjs.cloudflare.com/ajax/libs/d3/7.8.5/d3.min.js
    ```


3. Prepare your data. For this demo, we are using `happiness-sample-data.csv`. 

## Read data

4. Load the data onto the webpage with `d3.csv` or `d3.json` ([🔗 to doc](https://github.com/d3/d3-fetch/tree/v3.0.1)) 
    - You will be doing this inside the `script` tag inside `head`.


    ```
    d3.csv("your-data-file.csv")
        .then(data => {
          // check if the data is loaded:
          console.log(data)
          
          // == your code happens below ==
        })
    ```

## Create web elements and bind data to them


5. Create an overall SVG container for your graphic inside `#my-svg-chart` using `d3.select().append()`
    - Make sure you declare `width` and `height` for your SVG element with the chained `.attr()` function.
    - Avoid using `d3.create()` if you don't know what you are doing.
        
        ```
        const myChart = d3
                .select('#my-svg-chart')
                .append('svg')
                .attr('width', 640)
                .attr('height', 640)
        ```


6. Create shapes that you want to bind your data to, and bind the data to them. You will be using `d3.selectAll().data().join()`. 
    - You can create:
        - [Circles](https://www.w3schools.com/graphics/svg_circle.asp)
        - [Rectangles](https://www.w3schools.com/graphics/svg_rect.asp)
        - [Lines](https://www.w3schools.com/graphics/svg_line.asp)
        - [Text](https://www.w3schools.com/graphics/svg_text.asp)
        - ... (any other SVG elements)

    - This code example uses a rectangle.

        ```
        const individualCharts = myChart
            .selectAll('rect')
            .data(data)
            .join('rect');
        ```

7. Tweak the attributes of the SVG shapes to position them at the right places.


    ```
    const gridSize = 20, gap = 2; 

    // with SVG rectangle-specific attributes

    individualCharts
        .attr('x', (d,i) => {
            return Math.floor(i%10)*(gridSize+ gap);
        })
        .attr('y', (d,i) => {
            return Math.floor(i/10)*(gridSize+ gap);
        })
        .attr('width', gridSize)
        .attr('height', gridSize)
    ```

8. Encode data onto the SVG shapes using colors, sizes, directions, etc.

    ```
    individualCharts
        .style('fill', d=> {
            if (d.Happiness == '1') {return 'black'}
            if (d.Happiness == '2') {return 'grey'}
            if (d.Happiness == '3') {return 'gold'}
        });

    ```

You're done. Good job.

You can play around different SVG shapes/text/path, different ways of encoding your data...  
- Encode data as size instead of colors? Using different shapes or even text?
- Sort the data based on categories of variables?
- Change the position of the data to compare length?

... and don't forget to publish your page.
     


--- 

#### Additional resources on D3
- [Read the official doc](https://d3js.org/getting-started) and [the most important API](https://github.com/d3/d3/blob/main/API.md)
- [D3 gallery on Observable](https://observablehq.com/@d3/gallery) if you want to play around/ borrow the code.  
- [How to learn D3?](https://2019.wattenberger.com/blog/d3) An interactive tutorial by Amelia Wattenberger
- [Shirley Wu's Introduction to D3](https://observablehq.com/@sxywu/introduction-to-svg-and-d3-js?collection=@sxywu/introduction-to-d3-js), also on Observable
