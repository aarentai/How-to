# Interactive console
## tab completion
Type object name(`plan`) (followed by `.`), then press `Tab`, you can see all the properties and methods of the object.

## object and method properties
|        Type          |       Example       |
|:--------------------:|:-------------------:|
| object               | `AdaptationTo._`    |
| method               | `AddNewBeamSet(..)` |
| list of objects      | `BackupPlans[]._`   |
| immutable properties | `#IsBackupPlan`     |
- Type object name(`plan`) followed by `._`, then press `Enter`, you can get the names of all available properties, object and method of an object. 
And the suffix indicates the type of the object.

- Type object name(`plan`) followed by `._print`, then press `Enter`, you can get the value of each property and the number of items in each list of the object. 

- Type object name(`plan`) followed by `._help`, then press `Enter`, you can get documentation on an object or methods.

## state tree
Tyou can bring out the state tree for a patient by typing
```
import statetree
statetree.RunStateTree(True)
```
which is followed by a State Viewer window popping up.

Also, you can bring out the state tree for the machine of the current loaded beam set by typing
```
statetree.RunMachineStateTree(None, True)
```
which is also followed by a State Viewer window popping up.
Following are the methods to call state tree of databases.
|      Object      |             Instruction             |
|:----------------:|:-----------------------------------:|
| patient database | `statetree.RunPatientDBStateTree()` |
| machine database | `statetree.RunMachineDBStateTree()` |
| clinic database  | `statetree.RunClinicDBStateTree()`  |

# Common objects
## `get_current()`
|              Object             |                 Instruction                |
|:-------------------------------:|:------------------------------------------:|
| current loaded patient          | `patient = get_current('Patient')`         |
| current loaded case             | `case = get_current('Case')`               |
| current loaded plan             | `plan = get_current('Plan')`               |
| current loaded beam set         | `beam_set = get_current('BeamSet')`        |
| current loaded examination      | `examination = get_current('Examination')` |
| current loaded patient database | `patient_db = get_current('PatientDB')`    |
| current loaded machine database | `machine_db = get_current('MachineDB')`    |
| current loaded clinic database  | `clinic_db = get_current('ClinicDB')`      |

## patients
You can only get a handle to the patient that is currently loaded, which also means only one patient at a time.
```
patient_db      = get_current('PatientDB')
all_patients    = patient_db.QueryPatientInfo(Filter={})
mutable         = patient_db.QueryPatientInfo(Filter={'IsImmutable':False})
smiths          = patient_db.QueryPatientInfo(Filter={'LastName':'^Smith$'})
contain_smith   = patient_db.QueryPatientInfo(Filter={'LastName':'Smith'})
# load patient
patient_db.LoadPatient(PatientInfo=smiths[0])
```

## case
It's possible to access a case for the currently loaded patient wich is not the current loaded case.
```
patient = get_current('Patient')
case_name = 'Original'
try:
    case_to_load = patient.case[case_name]
except:
    print(f'No case named {case_name} exists for the current patient.')
case_to_load.SetCurrent()
```

## treatment plan
```
case = get_current('Case')
plan_name = 'IMRT'
try:
    plan_to_load = case.TreatmentPlans[plan_name]
except:
    print(f'No plan named {plan_name} exists for the current case.')
plan_to_load.SetCurrent()
```

## beam set
```
plan = get_current('Plan')
beam_set_name = '5 beam'
try:
    beam_set_to_load = plan.BeamSets[beam_set_name]
except:
    print(f'No beam set named {beam_set_name} exists for the current plan.')
beam_set_to_load.SetCurrent()
```