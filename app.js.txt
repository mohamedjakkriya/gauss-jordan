function createMatrix(){

    let size = document.getElementById("size").value
    let container = document.getElementById("matrixInput")

    let table = "<table>"

    for(let i=0;i<size;i++){
        table += "<tr>"

        for(let j=0;j<=size;j++){
            table += `<td><input type="number" id="a${i}${j}" value="0"></td>`
        }

        table += "</tr>"
    }

    table += "</table>"

    container.innerHTML = table
}


function solve(){

    let size = document.getElementById("size").value
    let matrix = []

    for(let i=0;i<size;i++){
        matrix[i] = []

        for(let j=0;j<=size;j++){
            matrix[i][j] = parseFloat(document.getElementById(`a${i}${j}`).value)
        }
    }

    for(let i=0;i<size;i++){

        let diag = matrix[i][i]

        for(let j=0;j<=size;j++){
            matrix[i][j] = matrix[i][j] / diag
        }

        for(let k=0;k<size;k++){

            if(k != i){

                let factor = matrix[k][i]

                for(let j=0;j<=size;j++){
                    matrix[k][j] -= factor * matrix[i][j]
                }

            }
        }
    }

    let result = ""

    for(let i=0;i<size;i++){
        result += `x${i+1} = ${matrix[i][size].toFixed(2)} <br>`
    }

    document.getElementById("result").innerHTML = result
}