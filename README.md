# 计算器
library(shiny)

ui <- fluidPage(
  titlePanel(em("指数基金收益计算器",style = "color: brown")),
  sidebarLayout(
    sidebarPanel(h2("紫薇组"),
                 p(span("R康", style = "color:red"),"不要难过,看到你这样难过,我的心里就会更加难过。"),
                 br(),
                 strong("团队成员：李红浪,张道琳,杨星雨,林臻杰,张欣（排名不分先后）"),
                 img(src= "photo.jpg" ,height=150, width=240),
                 br(),
                 br(),
                 br(),
                 p(strong("欢迎使用收益计算器。"),"该计算器可以根据历史数据计算在一段时间内定投某只基金取得的收益。您只需输入投资的基金、定投金额、定投期限等内容。本计算器会为您计算出：投资收益及收益率，并显示定投明细、费用明细等内容。"),
                 p("此APP主要运用R语言中的",a("{ Shiny } ",href = "https://shiny.rstudio.com"),),
                 img(src= "shiny.jpg" ,height=80, width=220),
                 br(),
                 p("数据来源于", span("Wind数据库", style = "color:red")),
                 div("<投资有风险，入市需谨慎>",style = "color:gray"),
                 
                 
    ),
    mainPanel(
      img(src= "shiny2.png" ,height=80, width=400),
      h2("指数基金收益计算器", align = "center"),
      br(),
      h5("CALCULATOR🧮"),
      code("*请在下列输入框中填入对应数字",),
      
      textInput(inputId = "index", label = "定投基金",value = "请输入基金代码六位数字"),
      dateInput(inputId = "date_1", label = "定投开始日", format = "yyyy-mm-dd", daysofweekdisabled=c(0,6)),
      dateInput(inputId = "date_2", label = "定投结束日", format = "yyyy-mm-dd", daysofweekdisabled=c(0,6)),
      dateInput(inputId = "date_3", label = "定投赎回日", format = "yyyy-mm-dd", daysofweekdisabled=c(0,6)),
      numericInput(inputId = "sect", label = "间隔日期" ,value = "1",min = "1"),
      sliderInput(inputId = "mon", label = "定投金额" ,value = "0",min =  0, max=10000,sep = ",",step = 100,post = "¥"),
      textOutput(outputId ="IRR" ),
      
    ),
  )
)


server <- function(input, output){
  output$IRR<- renderText(input$mon*input$sect)
  
}

shinyApp(ui = ui ,server = server)




