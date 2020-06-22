library(shiny)
library(shinydashboard)
library(dplyr) 
library(leaflet)
library(jsonlite)
library(geojsonio)
library(ggplot2)
library(plotly)
library(shinyWidgets)
library(RColorBrewer)
library(scales)
library(lattice)
library(DT)
library(packcircles)
library(rsconnect)


#choicee for drop-downs
vars <-names(df_map)
vars <-vars[-1:-2]

num <- names(df_plot)
num <- num[-8]




shinyUI(
  dashboardPage(
    dashboardHeader( title="World Health Systems"),
    dashboardSidebar(
      sidebarMenu(
        menuItem("Interactive Map", tabName="InteractiveMap", icon = icon("map")),
        menuItem("Region Plot", tabName="Regionplots", icon = icon("pie-chart")),
        menuItem("Data Explorer", tabName="DataExplorer", icon = icon("database")),
        menuItem("Documentation", tabName="Documentation", icon = icon("list")),
        menuItem("App Description", tabName="AppDescrption", icon = icon("desktop"))
      )
      ),
    dashboardBody(
      tabItems(
        
        tabItem(tabName = "InteractiveMap",
                div(
                  class="outer",
                  
                  tags$head(
                    # Include our custom CSS
                    includeCSS("styles.css"),
                    ##includeScript("gomap.js")
                  ),
                  
                  # If not using custom CSS, set height of leafletOutput to a number instead of percent
                  leafletOutput("map", width="100%", height="100%"),
                  
                  # Shiny versions prior to 0.11 should use class = "modal" instead.
                  absolutePanel(id = "controls", class = "panel panel-default", fixed = TRUE,
                                draggable = TRUE, top = 55, left = "auto", right = 10, bottom = "auto",
                                width = 440, height = "100%",
                                
                                h2("2017 World Development Indicators"),
                                
                                selectInput("variable", "Select the comparing variable:", vars),
                                
                                tableOutput("data")
                                
                  )
                )
                ),
        
        tabItem(tabName = "Regionplots",
                fluidRow(column(4, wellPanel(
                  #pickerInput("country", "Country:", c(as.character(df$Country)),
                   #                                   options = list(`actions-box` = TRUE),
                    #                  multiple = TRUE, selected = df$Country[[1]]),
                  
                  selectInput('num', 'Select comparing variable:', num, selected = num[[1]]),
                  
                  ),),
                  box(plotOutput(outputId = "plot1", width = "100%"))
               
                ),
        ),
        tabItem(tabName = "DataExplorer",
                fluidPage(column(4,selectInput("country", "Country:", c("All", unique(as.character(df$Country)))))),
                DT :: dataTableOutput("table")
                ),
        tabItem(tabName="Documentation",
                fluidRow(
                               box(h3("Health Expenditure"),
                                   tags$head(tags$style('h3{color:midnightblue;}')),
                                   (tags$img(src="img5.png", height=230,width=250)),
                                   p("The health expenditure estimates have been prepared by the World Health Organization under the framework of the System of Health Accounts 2011 (SHA 2011). The Health SHA 2011 tracks all health spending in a given country over a defined period of time regardless of the entity or institution that financed and managed that spending. It generates consistent and comprehensive data on health spending in a country, which in turn can contribute to evidence-based policy-making."),
                                   tags$style("h4{font-family:Roman;}"),
                                   tags$head(tags$style('h4{color:darkslategrey;}')),
                                   tags$style("h3{font-family:Arial;}"),
                                   ),
                                box(h3("Why is this study important?"),
                                    (tags$img(src="img1.png", height=230,width=250)),
                                    tags$head(tags$style('h4{color:darkslategrey;}')),
                                    tags$style("h3{font-family:Arial;}"),
                                    p("1. Helps to identify key issues such as weaknesses and strengths and areas that needs investment"),
                                    p("2. Promote, restore and maintain health system"),
                                    p("3. To improve the health stats of populations"),
                                    p("4. To increase the effectiveness of programs aimed at reducing specific diseases and further reduce morbidity and mortality"),
                                    p("5. Monitoring health systems allows the effectiveness, efficiency, and equity of different health system models to be compared"),
                                    
                                    ),
                               box(h3("What are the data used in this study?"),
                                   (tags$img(src="img2.png",height=230,width=250)),
                                   p("1. List of countries used by World Bank "),
                                   p("2. Level of current health expenditure expressed as a percentage of GDP"),
                                   p("3. Current expenditures on health per capita in current US dollars."),
                                   p("4. Physicians (per 1,000 people)"),
                                   p("5. Nurses and midwives (per 1,000 people) "),
                                   p("6. Specialist surgical workforce (per 100,000 population) "),
                                   p("7. Percentage of children under age 5 whose births were registered at the time of the survey"),
                                   p("8. Percentage of death registration with cause-of-death information ")
                                   
                                   ),
                               (tags$img(src="img3.png",height=230,width=250))
                                
                
                )
                ),
        tabItem(tabName = "AppDescrption",
                fluidPage(
                  mainPanel(
                    
                    box(h4("Interactive Map"),
                        tags$img(src="img6.png", width=450,height=300),
                        p("A choropleth map is used to display shaded areas representing an aggregate summary of various geographic characteristics particular to health systems such as % of GDP allocated to health expenditure, number of health workers and more. To view the result, user can select the characteristic variable from the drop down menu or click on a location in the map. Red is shown on locations with lower values while green is shown for higher values, as told by the color tile legend."),
                        width = 100
                    ),
                    box(h4("Region Plot"),
                        tags$img(src="img8.png", width=450,height=300),
                        p(" Health Systems is presented in bar plot.User can select the characteristic variable from the drop down  to view the value of different continents which are divided by eastern mediternan, europe, africa, americas,western pacific, south east asia."),
                        width = 100
                    ),
                    
                    box(h4("Data Explorer"),
                        tags$img(src="img7.png", width=450,height=300),
                        p(" Data from the World Development Indicators: Health Systems is presented in tabular format. User can use the “search” tab to explore for specific values from the dataset."),
                        width = 100
                    ),
                    
                    box(h4("Documentation"),
                        tags$img(src="img9.png", width=450,height=300),
                        p("Summary of the web application is presented here. The purpose of the study, the importance of the study and the data used in building this application can be found"),
                        width = 100
                        ),
                    h2("~~~ Thank you ~~~"),
                    
                    
                  )
                )
             
                )
      )
    )
  
    )
  )
