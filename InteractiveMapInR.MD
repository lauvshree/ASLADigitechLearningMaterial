## Lab: Creating an Interactive Map in R  

Welcome to the 2nd RStudio lab, in which we create an interactive map using two libraries. Shiny, which is an amazing library for prototyping interactive user interfaces in R and Leaflet which allows us to use OpenStreetMap data to create an interactive map. Shiny will use Leaflet as one of it’s UI components (like any other UI component like button, slider or text field).

1. Install the following packages, you can do so by simply paste and execute the following command into the bottom left Console window

```
install.packages("shiny")

install.packages("leaflet")
```

https://d3c33hcgiwev3.cloudfront.net/imageAssetProxy.v1/gvW_F-uRT-q1vxfrkW_qkg_6d5318986a6786bfd5b1366b0c14bea3_Lab_2.3.6_-1.png?expiry=1591401600000&hmac=HQoA7y21RH3K0kowxm387lhrusTsIe90rzDL9yk130c

2. Paste the following code into a new R edit window in RStudio:

```
library(shiny)
library(leaflet)

r_colors <- rgb(t(col2rgb(colors()) / 255))
names(r_colors) <- colors()

ui <- fluidPage(
        leafletOutput("mymap"),
        p(),
        actionButton("recalc", "New points")
    )

server <- function(input, output, session) {
            points <- eventReactive(input$recalc, {
                points = cbind(rnorm(40) * 2 + 13, rnorm(40) + 48)

                #Insert code here 

                return(points)}, ignoreNULL = FALSE)

        observeEvent(input$Map_shape_click, { # update the location selectInput on map clicks
            output$coordinates <- renderText({ 
                "You have selected this"
            })
            })
        output$mymap <- renderLeaflet({
            leaflet() %>%
            addProviderTiles(providers$Stamen.TonerLite,
            options = providerTileOptions(noWrap = TRUE)
            ) %>%
            addMarkers(data = points())
        })

}

shinyApp(ui, server)
```

3. Click on the Run App button
https://d3c33hcgiwev3.cloudfront.net/imageAssetProxy.v1/JeB6Ao4tSZagegKOLamWJQ_fccd4347c2b7076641a1fb1594ee940a_Lab_2.3.6_-2.png?expiry=1591401600000&hmac=xgGymRV9XBxc11TZZjcCmEOio-0Gn3DtaWPk1vyDeqo

You’ll see the following application appear:

https://d3c33hcgiwev3.cloudfront.net/imageAssetProxy.v1/XM-3OCPsSQWPtzgj7FkFVA_bbb84416e89a5fcdb60e8e20ca5e033f_Lab_2.3.6_-3.png?expiry=1591401600000&hmac=n3gN5qA3xOPHB_hwZbPhlxLJHxMFZqzr2thBLZkRR2U

4. If you click New points, a new set of random points will be generated and displayed. 

5. Now let's change the code to display the list of points on the user interface. 
6. Then, it is time to also change the behavior of this application by changing the “server” object. Therefore, please add the following three lines to the so-called “eventhandler” responsible to execute code if the button is clicked:   

Replace the code here under

```

ui <- fluidPage(	
  leafletOutput("mymap"),	
  p(),	
  actionButton("recalc", "New points")	
)

```

with 

```
ui <- fluidPage(
  leafletOutput("mymap"),
  p(),
  actionButton("recalc", "New points"),
  p(),
  textOutput("coordinates")
)
```

and also replace 

```
points <- eventReactive(input$recalc, {	
    points = cbind(rnorm(40) * 2 + 13, rnorm(40) + 48)	
    return(points)	
  }, ignoreNULL = FALSE)

```

with 

```
points <- eventReactive(input$recalc, {    
    points = cbind(rnorm(40) * 2 + 13, rnorm(40) + 48)    
    output$coordinates <- renderText({       
      points      
    })    
    return(points)    
  }, ignoreNULL = FALSE)

```

such that the complete code section looks like this:         

```
library(shiny)

library(leaflet)

r_colors <- rgb(t(col2rgb(colors()) / 255))

names(r_colors) <- colors()

ui <- fluidPage(  
  leafletOutput("mymap"),  
  p(),  
  actionButton("recalc", "New points"),  
  p(),  
  textOutput("coordinates")  
)

server <- function(input, output, session) {
  
  points <- eventReactive(input$recalc, {    
    points = cbind(rnorm(40) * 2 + 13, rnorm(40) + 48)    
    output$coordinates <- renderText({       
      points      
    })    
    return(points)    
  }, ignoreNULL = FALSE)
    
  observeEvent(input$Map_shape_click, { # update the location selectInput on map clicks    
    output$coordinates <- renderText({       
      "You have selected this"      
    })    
  })
  
  output$mymap <- renderLeaflet({    
    leaflet() %>%      
      addProviderTiles(providers$Stamen.TonerLite,                       
                       options = providerTileOptions(noWrap = TRUE)                       
      ) %>%      
      addMarkers(data = points())    
  })  
}

shinyApp(ui, server)
```

7. If you now re-run this application, you’ll notice a list of coordinate pairs which updates every time you click the New points button

https://d3c33hcgiwev3.cloudfront.net/imageAssetProxy.v1/1GEOJe-NSh6hDiXvjboeFw_0a7e289009f425fce62bf449f05e7847_Lab_2.3.6_-4.png?expiry=1591401600000&hmac=Kn0-J4tY3SA8TFRnGGhU-H7SsDxjCUuNer4OASGthcY

This concludes this lab, we hope that you had fun! If you want to know more about Shiny and Leaflet, please visit the following links:

https://shiny.rstudio.com/

https://rstudio.github.io/leaflet/

