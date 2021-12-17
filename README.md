# DwellingClassesLearningKotlin
A program that gets the number of residents for a dwelling and calculates its floor area + the carpet size for that particular place.

import kotlin.math.PI
import kotlin.math.sqrt

fun main(){
    val squareCabin = SquareCabin(6, 50.0)
    val roundHut = RoundHut(3, 10.0)
    val roundTower = RoundTower(4, 2, 15.5)
    
    with(roundHut){
        println("Information about Round Hut")
        println("Capacity: ${capacity}")
        println("Building Material: ${buildingMaterial}")
        println("Has Room? ${hasRoom()}")
        println("Floor area: %.2f".format(floorArea()))
        println("Has room? ${hasRoom()}")
        getRoom()
        println("Has room? ${hasRoom()}")
        getRoom()
        println("Carpet size: ${calculateMaxCarpetSize()}")

    }
    print("\n\n")
    with(squareCabin){
        println("Information abaout Square Cabin")
        println("Capacity: ${capacity}")
        println("Building Material: ${buildingMaterial}")
        println("Has Room? ${hasRoom()}")
        println("Floor Area: ${floorArea()}")
    }
    println("\n\n")
    with(roundTower){
        println("Information about Round Tower")
        println("Capacity: ${capacity}")
        println("Building Material: ${buildingMaterial}")
        println("Has Room? ${hasRoom()}")
        println("Floor area: ${floorArea()}")
		println("Carpet size: ${calculateMaxCarpetSize()}")
    }
}


abstract class Dwelling(private var residents: Int){
    abstract val buildingMaterial: String
    abstract val  capacity: Int
    abstract fun floorArea(): Double

    fun hasRoom(): Boolean{
    	if (residents < capacity){
    		return true
    	}
        else{
    		return false
		}
	}
    fun getRoom(){
        if (capacity > residents){
            residents++
            println("You Got a New Room!")
        }else{
            println("Unfortunately the Rooms are all Full..")
        }
    }
}
    
class SquareCabin(residents: Int, val length: Double): Dwelling(residents){
	override val buildingMaterial = "Wood"
	override val capacity = 6
    override fun floorArea(): Double{
        return length * length
    }
}

open class RoundHut(val residents: Int, val radius: Double): Dwelling(residents){
    override val buildingMaterial = "Straw"
    override val capacity = 4
    override fun floorArea(): Double{
        return PI * radius * radius
    }
    fun calculateMaxCarpetSize(): Double{
        val diameter = 2 * radius
        return sqrt(diameter * diameter / 2)
    }
}

class RoundTower(residents: Int,
                 val floors: Int = 2,
                 radius: Double): RoundHut(residents, radius){
    override val buildingMaterial = "Stone"
    override val capacity = 4 * floors
    override fun floorArea(): Double{
        return super.floorArea() * floors
    }
}
