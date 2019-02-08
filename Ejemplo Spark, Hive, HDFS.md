## Ejercicio Spark, Hive, HDFS 

//
```
import org.apache.spark.sql.SQLContext
import org.apache.spark.sql.types
import org.apache.spark.sql._
import spark.implicits._
```

// crear SparkSession
```
val spark = 
SparkSession.builder()
.enableHiveSupport()  // Activar el soporte para Hive
.getOrCreate()
```

// crear tabla y declarar el almacenamiento como orc
```
spark.sql("CREATE TABLE yahoo_orc_table (date STRING, open_price FLOAT, 
high_price FLOAT, low_price FLOAT, close_price FLOAT, volume INT, adj_price FLOAT) stored as orc")

// pasar datos a RDD

val yahoo_stocks = sc.textFile("/tmp/yahoo_stocks.csv")

// crear la clase
case class YahooStockPrice(date: String, open: Float, high: Float, low: Float, close: Float, volume: Integer, adjClose: Float)

// parsear datos y convertir a DataFrame
val stockprice = data.map(_.split(",")).map(row => YahooStockPrice(row(0), row(1).trim.toFloat,
row(2).trim.toFloat, row(3).trim.toFloat, row(4).trim.toFloat, row(5).trim.toInt, row(6).trim.toFloat)).toDF()

// crear vista
stockprice.createOrReplaceTempView(yahoo_stocks_temp)

// seleccionar datos
val results = spark.sql("SELECT * FROM yahoo_stocks_temp")

// imprimir resultados
results.map(t => "Stock Entry: " + t.toString).collect().foreach(println)
```
Almacenar y leer los datos
```
results.write.format("orc").save("yahoo_stocks_orc") // almacenamiento en carpeta spark

results.write.format("orc").save("/apps/hive/warehouse/yahoo_stocks_orc") // almacenamiento en carpeta hive

val yahoo_stocks_orc = spark.read.format("orc").load("yahoo_stocks_orc") // cargar los datos de nuevo

```
