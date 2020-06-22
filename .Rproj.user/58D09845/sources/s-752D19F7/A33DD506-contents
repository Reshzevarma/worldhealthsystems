library(shiny)
library(shinydashboard)
library(dplyr)
library(leaflet)
library(ggplot2)
library(rlang)
library(plotly)
library(RColorBrewer)
library(scales)
library(lattice)
library(hues)
library(ggeasy)
function(input, output, session){
  #variable
  target_quo = reactive ({
    parse_quosure(input$variable)
  })
  
  dftable<- reactive ({
    df_map%>%
      arrange(desc(!!target_quo()))
  })
  
  dfmap<- reactive ({
    df_map%>%
      select(input$variable)
  })
  
  # Create the map
  output$map <- renderLeaflet({
    leaflet(geojson) %>% 
      addTiles(urlTemplate = "//{s}.tiles.mapbox.com/v3/jcheng.map-5ebohr46/{z}/{x}/{y}.png",
               attribution = 'Maps by <a href="http://www.mapbox.com/">Mapbox</a>')%>%
      addPolygons(stroke = FALSE, smoothFactor = 0.3, fillOpacity = 0.5,
                  label = paste(df_map$Country, ":", dfmap()[,1]),
                  color = pal(rescale(dfmap()[,1],na.rm=TRUE))
                  
                  
      )%>%
      setView(lng = 0, lat = 40, zoom = 2) %>%
      addLegend("bottomleft",pal = pal, 
                values =c(0:1), opacity = 0.5)
  })
  
  output$data <- renderTable({
    head((dftable()[, c("Country", input$variable), drop = FALSE]) ,10)
  }, rownames = TRUE)
  
  
  #Create the data explorer
  output$table <- DT::renderDataTable({
    if(input$country != "All"){
      df <- df[df$Country == input$country,]
    }
    DT::datatable(df)
    
  })

agg = aggregate(.~df_cont, df_plot, mean) 

output$plot1 <- renderPlot({
if(input$num == "Health.GDP."){

  ggplot(data=agg, aes(x=df_cont, y= agg$Health.GDP.)) +
    geom_bar(stat="identity",width = 0.8, fill = rainbow(6))+
    geom_point(col = rainbow(1))+
    ggtitle("Health GDP")+
    labs(x="Continent", y="Health GDP")+
    theme_classic()
}

else if(input$num == "Health.Expenditure."){
    ggplot(data=agg, aes(x=df_cont, y= agg$Health.Expenditure.)) +
    geom_bar(stat="identity",width = 0.8, fill = rainbow(6))+
    geom_point(col = rainbow(1))+
    ggtitle("Health Expenditure")+
    labs(x="Continent", y="Health Expenditure")+
    theme_classic()
}

else if(input$num == "Physiciansper1000people"){
    ggplot(data=agg, aes(x=df_cont, y= agg$Physiciansper1000people)) +
    geom_bar(stat="identity",width = 0.8, fill = rainbow(6))+
    geom_point(col = rainbow(1))+
    ggtitle("Physiciansper1000people")+
    labs(x="Continent", y="Physiciansper1000people")+
    theme_classic()
}
  
else if(input$num == "Nurses_Midwivesper1000people"){
    ggplot(data=agg, aes(x=df_cont, y= agg$Nurses_Midwivesper1000people)) +
    geom_bar(stat="identity",width = 0.8, fill = rainbow(6))+
    geom_point(col = rainbow(1))+
    ggtitle("Nurses_Midwivesper1000people")+
    labs(x="Continent", y="Nurses_Midwivesper1000people")+
    theme_classic()
}

else if(input$num == "Specialist.Surgeonsper10000people"){
    ggplot(data=agg, aes(x=df_cont, y= agg$Specialist.Surgeonsper10000people)) +
    geom_bar(stat="identity",width = 0.8, fill = rainbow(6))+
    geom_point(col = rainbow(1))+
    ggtitle("Specialist.Surgeonsper10000people")+
    labs(x="Continent", y="Specialist.Surgeonsper10000people")+
    theme_classic()
  }
  
  
else if(input$num == "Registered.Births."){
    ggplot(data=agg, aes(x=df_cont, y= agg$Registered.Births.)) +
    geom_bar(stat="identity",width = 0.8,fill = rainbow(6))+
    geom_point(col = rainbow(1))+
    ggtitle("Registered.Births")+
    labs(x="Continent", y="Registered.Births")+
    theme_classic()
} 
  
else if(input$num == "Registered.Deaths."){
    ggplot(data=agg, aes(x=df_cont, y= agg$Registered.Deaths.)) +
    geom_bar(stat="identity",width = 0.8,fill = rainbow(6))+
    geom_point(col = rainbow(1))+
    ggtitle("Registered.Deaths")+
    labs(x="Continent", y="Registered.Deaths")+
    theme_classic()
  }

})
}


