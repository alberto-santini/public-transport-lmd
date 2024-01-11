# Integrating Public Transport in Sustainable Last-mile Delivery: Column Generation Approaches

This repository contains the instances and the solutions presented in the following paper:
```bib
@techreport{delle_donne_et_al,
    title={Integrating Public Transport in Sustainable Last-mile Delivry: Column Generation Approaches},
    author={{Delle Donne}, Diego and Santini, Alberto and Archetti, Claudia},
    year={2024},
    url={...}
}
```

You can also cite this repository through Zenodo:
```bib
@misc{delle_donne_et_al_instances,
    title={Instances and Results for the Paper ``Integrating Public Transport in Sustainable Last-mile Delivry: Column Generation Approaches''},
    author={{Delle Donne}, Diego and Santini, Alberto and Archetti, Claudia},
    year={2024},
    doi={...},
    url={...}
}
```

![](banners/banner1.png)

## Datasets

The repository contains two datasets:

* Instances in folder `mandal_and_archetti` are from the following paper and are used for comparison with the method proposed by the paper's authors.
```bib
@misc{mandal_archetti,
    title={A Decomposition Approach to Last Mile Delivery Using Public Transportation Systems}, 
    author={Minakshi Punam Mandal and Claudia Archetti},
    year={2023},
    eprint={2306.04219},
    archivePrefix={arXiv},
    primaryClass={math.OC}
}
```
* Instances in folder `delle_donne_et_al` were generated specifically for our paper. We used them as a testbed for our algorithms and to test the effectiveness of the approaches we proposed.

![](banners/banner2.png)

## Results

Results are provided in the `.csv` format.
File `delle_donne_instances.csv` constains the results for the instances of folder `delle_donne_et_al`.
File `mandal_instances.csv` contains the results for the instances of folder `mandal_et_archetti`.

![](banners/banner3.png)

## Instance format

Each instance is described by three files.

### The `.city` file

The `.city` file describes the characteristics of stops, customers, and transit lines.

#### Stops

Lines starting with `S` describe stops. Each line describes a stop, and contains:
* The name (field `name`).
* The capacity (field `capS`).
* Field `capI` can be ignored.
* Field `capO` can be ignored.
* Field `cost` can be ignored.
* The x coordinate (field `x`).
* The y coordinate (field `y`).
* The service time (field `Ts`).
* The maximum wait time of a parcel (field `Wmax`).

#### Consolidation and Distribution Centre

Lines starting with `O` describe the Consolidation and Distribution Centre (CDC).
In our instances, there is only one CDC, and it is decribed by:
* Its name (field `name`).
* Its x coordinate (field `x`).
* Its y coordinate (field `y`).

The line following the CDC description lists all stops that can be reached from it.
By definition, these are the in-stops; all other stops are out-stops.

#### Customers

Lines starting with `D` describe customers.
Each customer has the following associated fields:
* The name (field `name`).
* The x coordinate (field `x`).
* Its y coordinate (field `y`).

The line following each customer description lists which out-stops can be used to serve the customer.

#### Public Transport Lines

Lines starting with `F` describe public transport lines.
Each public transport line is described by the following data:
* The name (field `name`).
* The fleet name (field `fleetname`). It can be ignored.
* The vehicle capacity (field `cap`).
* Field `cost` can be ignored.
* The time when the first vehicle of the line reaches the first stop in its sequence (field `first_bus`).
* The interval between two consecutive buses of the line (field `frequency`).
* The number of daily runs (field `nBuses`).

The line following each public transport line's description is the sequence of visited stops.
To compute the bus arrival times at the stops, consider a speed equal to 0.2 times the euclidean distance between successive stops.

### The `.demands` file

The `.demands` file gives further informations about the clients.
The first field of each line is the customer's name; the second is the customer's demand; the third and fourth field are the start and end time of the customer's time window.

### The `.params` file

The `.params` file contains other instance information.
Field `Lmax` is the maximum duration of a courier's route.
Field `maxTrucks` is the truck fleet size.
Field `maxFreightersPerStop` is the number of couriers available at each out-stop.
Field `trucksCap` is the truck's capacity.
Field `freighterCap` is the courier's capacity.