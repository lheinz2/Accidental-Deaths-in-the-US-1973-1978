# Accidental-Deaths-in-the-US-1973-1978
library(shiny)

source(Us.AccDeaths)
data.frame(Us.AccDeaths)
ui1 <- fluidPage(
  titlePanel("Accidental Deaths in the US 1973-1978"),
  
  sidebarLayout(
    
    sidebarPanel(
      
      selectInput("month",
                  "Month:",
                  c("January" = "Jan",
                    "February" = "Feb", 
                    "March" = "Mar",
                    "April" = "Apr",
                    "May" = "May",
                    "June" = "Jun",
                    "August" = "Aug",
                    "September" = "Sep",
                    "October" = "Oct", 
                    "November" = "Nov",
                    "December" = "Dec"))
    ),
    
    mainPanel(
      
      plotOutput("AccPlot")
    )
  )
)


server2 <- function(input, output) {
  output$AccPlot <- renderPlot({
    
    plot(Us.AccDeaths$Years, Us.AccDeaths[,input$month], type = "o")
    main="Accidental Deaths in the US"
    ylab="Deaths in Selected Month"
    xlab="Year"
  })
}


# Run the application 
shinyApp(ui1, server2)
