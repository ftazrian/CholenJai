const container = document.querySelector(".container");
const seat = document.querySelector(".row .seat:not(.sold)");
const count = document.getElementById("count");
const total = document.getElementById("total");
const BusSelect = document.getElementById("Bus");

populateUI();

let ticketPrice = +BusSelect.nodeValue;

function setBusDate(BusIndex, BusPrice){
    localStorage.setItem("selectedBusIndex", BusIndex);
    localStorage.setItem("selectedBusPrice", BusPrice);
}
function updateSelectCount(){
    const selectedSeats = document.querySelectorAll('.row. seat.selected');

    const setIndex = [...selectedSeats].map(seat => [...seat].indexOf(seat))

    localStorage.setItem('selectedSeats' ,JSON.stringify(setIndex))

    const selectedSeatCount = selectedSeats.length

    count.innerText = selectedSeatCount
    total.innerText = selectedSeatCount * ticketPrice

    setBusDate(BusSelect.selectedIndex,BusSelect.value)
}

function populateUI() {
    const selectedSeats = JSON.parse(localStorage.getItem("selectedSeats"));

    if(selectedSeats !== null && selectedSeats.length > -1){
        selectedSeats.forEach((seat,index)=>{
            if(selectedSeats.indexOf(index) > -1){
                seat.classList.add("selected");
                

            }
        });
    }

    const selectedBusIndex = localStorage.getItem("selectedBusIndex");

    if(selectedBusIndex !== null) {
        BusSelect.selectedIndex = selectBusIndex;
    }
}

BusSelect.addEventListener("click", (e) => {
    if(
        e.target.classList.contains("seats") &&
        !e.target.classList.contains("sold")
    ) {
        e.target.classList.toggle("selected");

        updateSelectCount();
    }
})