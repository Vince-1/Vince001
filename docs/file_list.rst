for function
=============

cli
---

:ref:`cli`

main.py
^^^^^^^
* auto_sub()
* load_config(filename, is_no_config, dryrun)
* pygate(config, no_config, dryrun)


analysis.py
^^^^^^^^^^^
* analysis_kernel(source, target, analysis_type, dryrun)
* predefined(name, source, output)
* script(target, source, output):

clean.py
^^^^^^^^^
* clean_kernel(is_subdirectories, subdirectory_patterns: Iterable[str],
                 root_file_patterns: Iterable[str],
                 is_slurm_outputs, dryrun: bool)
* clean(subdirectories, root_files, slurm_outputs)

initialize.py
^^^^^^^^^^^^^
* init
* generate
    + mac_template(filename)
    + shell_task_list(tasks)
    + shell_run(filename,tasks,gate_version,shell,partition)
    + shell_post_run(filename,tasks,gate_version,shell,partition)
    + shell_post_run(filename,tasks,gate_version,shell,partition)
    + shell()
    + cfg(target,format)
    + subdir(nb_split,sub_format)
    + broadcast_kernel(files,subdirectory_patterns,dryrun)
    + bcast(target, no_ext)
    + external_to_copy()
    + ext()
    + auto()

mac_generate.py
^^^^^^^^^^^^^^^
* mac()
    + script()
    + predefined()

merge.py
^^^^^^^^
* Tasks
    + __init__(self,filename,method)
* merge_kernel(tasks:Iterable[Taks], subdir_pattern: Tterable[str],dryrun)
* merge(target, method)

submit.py
^^^^^^^^^
* Task
    + __init__(self, broadcast=None,single=None)
* submit_kernel(taks:Iterable[Task],subdir_patterns:Iterable[str],duyrun)
* submit(broadcast,single)




analysis
--------

:ref:`analysis`

__init__.py
^^^^^^^^^^^

predifined.py
^^^^^^^^^^^^^
* gamma_energy_deposite_distribution(csv_filename, h5_filename)

results.py
^^^^^^^^^^
* ParticleID(Enum)
* ColumnNames
* ResultBase
    + __init__(self,data=None)
    + d(self)
* Results(Resultbase)
    + __init__(self,data:Tuple[ResultBase])
    + map(self,func) -> 'Results'
    + fileter(self,func) -> 'Results'
    + call(self, fuc_name) -> 'Results'
    + zip(self, r: 'Results')
    + first(self) -> ResultBase
    + flatten(self) -> 'Results'
    + merge(self) ->ResultBase
    + to_list(self)
* ResultsDask(ResultBase)
* ResulltsNamedTuple(ResultBase)
* ResultsWithKeys(Results)
    + __init__(self,data: Tuple[Tuple[str,ResultBase]]
    + drop_keys(self) -> Results
    + to_dict(self)
    + select(self,key)
* ResultsWithUnknownKeys(ResultsDask)
    + select(self,key)
    + drop_keys(self) -> ResultsDask
* Series(ResultBase)
    + __init__(self,series: pd.Series)
    + columns(self, *cols)
    + position(self) -> 'Vec3'
    + source_position(self) ->'Vec3'
    + energy_deposit(self) -> float
* DaraFrame(ResultBase)
    + __init__(self, dataframe: pd.DataFrame)
    + first(self, *columns) -> Series
    + split_row(self) -> Results
    + merge(self, r) -> 'DataFrame'
    + to_event(self) -> 'Event'
* Vec3(ResultBase)
    + __init__(self, x, y=Mone, z=None)
    + x(self) -> float
    + y(self) -> float
    + z(self) -> float
    + to_list(self)
* EnergyDeposit(ResultBase)
    + def __init__(self, position,energy)
    + position(self)
    + energy(self)
* Event(DataFrame)
    + __init__(self,dataframe: pd.DataFrame)
    + source_position(self) -> Vec3
    + first_position(self) -> Vec3
    + incident_direction(self) -> Vec3
    + energy_deposit_list(self) -> Results
* CSVFile(ResultBase)
    + __init__(self,filename:str)
    + load(self) -> DataFrame



api
---

:ref:`api`

cli
^^^

 __init__.py
~~~~~~~~~~~~

base.py
~~~~~~~~
* CLI(click.MultiCommand)
    + __init__(self)
    + list_commands(self,ctx)
    + get_command(self, ctx, name)

commands.py
~~~~~~~~~~~
* _load_config(config)
* make_config()
* init(config,content)
* submit(config)
* merge(config)
* clean(config, content, dryrun)



archive
-------

:ref:`archive`


components
----------

:ref:`components`

geometry
^^^^^^^^

geometry.py
~~~~~~~~~~~
* GeometryPreInitialise(ObjectWithTemplate)
    + __init__(self, world:Volume)
* GeometryPostInitialise(ObjectWitheTempate)
    + __init__(self, surfaces)
* Gemetry
    + __init__(self, world:Volume)
    + render_pre(self)
    + render_post(self)

phantom.py
~~~~~~~~~~
* Phantom(ObjectWithTemplate)
    + __init__(self, sensitive_detectors: Tuple[Volume]=())

surface.py
~~~~~~~~~~
* Surface(ObjectWithTemplate)
    + __init__(self, base: Volume, insert:Volume)
* SurfaceOerfectAPD(Surface)
* SurfaceRoughTeflonWrapped(Surface)

volume.py
~~~~~~~~~
* Repeater(ObjectWithTemplate)
* RepeaterRing(Repeater)
    + __init__(self, number)
* RepeaterLinear(Repeater)
    + __init__(self, number, repeat_vector)
* RepeaterCubic(Repeater)
    + __init__(self, scale: Vec3, repeat_vector: Vec3)
* Volume(ObjectWithTemplate)
    + __init__(self, name, ,aterial=None, mother=None, position=None, unit=None, repeaters: Repeater=None)
    + add_child(self, child)
* Box(Volume)
    + __init__(self, name, size, material=None, ,other=None, position=None,unit=None,repeaters: Repeater=None)
* Cylinder(Volume)
    + __init__(self, name, rmax, rmin=None, height=None,phi_start=None,delta_phi=NOne,material=None,mother=None,position=None,unit=None,repeaters: Repeater=None)
* Sphere(Volume)
    + __init__(self, name, rmax, rmin=None, phi_start=None,delta_phi=None,theta_start=None,delta_theta=None,material=None,mother=None,position=None,unit=None,repeaters:Repeater=None)
* ImageRegularParamerisedVolume(Volume)
    + __init__(self, name, image_file, range_file, material=None,mother=None,position=None, init=None,repeaters: Repeater=None)
* Patch(Volume)
    + __init__(self, name, patch_file, material=None,mmother=None,position=None, unit=None, repeater:Repeater=None)

camera
~~~~~~

__init__.py
###########

camera.py
#########
* Camera(ObjectWithTemplate)
    + __init__(self, system:System, sensitive_detectors:Tuple[Volume]=())

system.py
#########
* System
    + __init__(self)

* PETscanner(System)
    + __init__(self,level1, level2, level3, level4, level5, sensitive_detectors=None)
* Ecat(System)
    + __init__(self, block=None, crystal=None)
* CylindricalPET(System)
    + __init__(self, rsector=None, module=None,submodule=None,crystal=None,layer0=None,layer1=None,layer2=None,layer3=NOne)
* MultiPatchPET(System)    
    + __init__(self, container, patch_list)
* SPECThead(System)
    + __init__(self,crystal,pixel=None)
* OpticalSystem(System)
    + __init__(self, crystal,pixel = None)


template
^^^^^^^^

digitizer
~~~~~~~~~

* singles
    + blurring.j2
    + buffer.j2
    + dead_time.j2
    + holder.j2
    + readout.j2
    + singles.j2
* co_incidence_chain.j2
* co_incidence_sorter.j2
* insertable.j2

geometry
~~~~~~~~

* volume
    + repeater
        - cubic.j2
        - linear.j2
        - repeater.j2
        - ring.j2
    + box.j2
    + cylinder.j2
    + image_sphere.j2
    + sphere.j2
    + volume.j2

* camera.j2
* geometry_post_init.j2
* geometry_pre_init.j2
* phantom.j2
* surface.j2
* system.j2

misc
~~~~

* database.j2
* verbose.j2
* visualisation.j2

parameter
~~~~~~~~~

* aquisition
    + aquisition.j2
    + period.j2
    + primaries.j2
* output
    + output.j2
    + root.j2
    + sinogram.j2
* random_engine
    + random_engine.j2
* parameter.j2

physics
~~~~~~~

* cuts.j2
* list.j2
* model.j2
* physics.j2
* procrss.j2


source
~~~~~~

* angular
    + angular.j2
    + iso.j2
* particle
    + gamma.j2
    + particle
    + position.j2
* shape
    + annulus.j2
    + circle.j2
    + cylinder.j2
    + ellipse.j2
    + ellipsoid.j2
    + rectangle.j2
    + shape.j2
    + sphere.j2
    + voxelized.j2
    
* source_list.j2
* source.j2

simulation.j2
~~~~~~~~~~~~~

test.j2
~~~~~~~

utils.j2
~~~~~~~~

vec3.j2
~~~~~~~

__init__.py
^^^^^^^^^^^

base.py
^^^^^^^
* ObjectWithTemplate(ObjectWithTemplateBase)
* Renderable
    + render(self) -> str

digitizer.py
^^^^^^^^^^^^

* Insetable(ObjectWithTemplate)
    + __init__(self, name=None, is_define_name=False, is_explicit_insert=True)
* Singles(Insertable)
    + __init__(self, plugins=None, name='Singles', is_define_name=False,is_explicit_insert=False)
* AdderCompton(Insetable)
    + __init__(self, name='adderCompton', is_define_name=False)
* Readout(Insertable)
    + __init__(self,policy=None,depth=1,name='readout',is_define_name=False)
* Blurring(Insertable)
    + __init__(self, law=None, resolution=0.15,eor=511, slope=None, name='blurring', is_define_name=False)
* Holder(Insetable)
    + __init__(self,value,name=None, is_define_name=False)
* ThresHolder(Holder)
    + __init__(self, value, name='thresHolder')
* UpHolder(Holder)
    + __init__(self, value, name='upholder')
* TimeResolution(Insetable)
    + __init__(self, resolution, name=None, is_define_name=False)
* WithBuffer(Insertable)
    + __init__(self, size=NOne, mode=NOne, name=NOne, is_define_name=False)
* MemoryBuffer(WithBuffer)
    + __init__(self, read_freq=NOne,size=None,mode=None,name=None,is_define_name=False)
* DeadTimeMulti(WithBuffer)
    + __init__(self, volume ,t , mode=None, buffer_size=None, buffer_mode=None, name='deadtime', is_define_name=False)
* SingleChain(Singles)
    + __init__(self, name, is_define_name=True)
* CoincidenceSorter(Insertable)
    + __init__(self, input_=None,window=NOne,offset=None,name='Coincidences',is_define_name=False, is_explicit_insert=False)
* CoincidencesChanin(Insertable)
    + __ini__(self,input1,input2,name,plugins=None,use_priority=None,conseve_all_event=None, is_define_name=True)

misc.py
^^^^^^^

* Verbose(ObjectWithTemplate)
    + __init__(self, physics=0,cuts=0,sd=0,action2=0,actor=0,step=0,error=0,warning=0,output=0,beam=0,volume=0,image=0,geometry=0,core=0,run=0,event=0,tracking=0)
* MateriaDatabase(ObjectWithTemplate)
    + __init__(self, path: str=None)
* MaterialDatabaseLocal(MaterialDatabase)
    + __init__(self)
* Visualisation(ObjectWithTemplate)
    + __init__(self, is_disable=True)

parameter.py
^^^^^^^^^^^^

* Acquisition(ObjectWithTemplate)
* AcquisitionPrimaries(Acquisition)
    + __init__(self,number=10000)
* AcquisitionPeriod(Acquisition)
    + __init__(self, start=0.0,end=1.0,step=1.0)
* Output(ObjectWithTemplate)
    + __init__(self,file_name)
* Ascii(Output)
    + __init__(self, file_name, hit=0, singles=0, coincidences=0)
* Binary(Output)
    + __init__(self,file_name,hit=0,singles=0, coincidence=0)
* Root(Output)
    + __init__(self,file_name，hit=None,singles=None,coincidences=None,optical=None,delay=NOne)
* Sinogram(Output)
    + __init__(self,file_name,input_,radial_bin=None,is_true_only=None,is_raw_output=NOne,tang_blurring=NOne,is_store,delay=None,si_store,scatter=None)
* RandomEngine(ObjectWithTemplate)
    + __init__(self,seed='default')
* RandomEngineRanlux64(RandomEngine)
* RandomEnginJamesRandom(RandomEngine)
* RandomEngineMersenneTwister(RandomEngine)
* Parameter(ObjectWithTemplate)
    + __init__(self,random_engine,outputs: List[output],acquisition)


physics.py
^^^^^^^^^^

* Model(ObjectWithTemplate)
    + __init__(self,particle=None)
* PenelopeModel(Model)
* StandarModel(Model)
* LivermoreModer(Model)
* LivermorePolarizeModel(Model)
* PhysicsProcess(ObjectWithTemplate)
    + __init__(self, models=NOne)
    + content_in_adding(self)
* PhotoElectric(PhysicsProcess)
* Compton(PhysicProcess)
* GammaConversion(PhysicsProcess)
* RayleighScattering(PhysicsProcess)
    + __init__(self, models=(PenelopeModel(),))
* ElectronIonisation(PhysicsProcess)
    + __init__(self, models=(StandardModel('e-'),StandardModel('e+')))
* Bremsstrahlung(PhysicsProcess)
    + __init__(self,models=(StandardModel('e-'),StandardModel('e+')))
* PhysicsProcessWithoutModels(PhysicsProcess)
    + __init__(self)
* PositronAnnihilation(PhysicsProcessWithoutModels)
* RadioactiveDecay(PhysicsProcessWithoutModels)
* OpticalAbsorption(PhysicsProcessWithoutModels)
* OpticalRayleigh(PhysicsProcessWithoutModels)
* OpticalBoundary(PhysicsProcessWithoutModels)
* OpticalMie(PhysicsProcessWithoutModels)
* OpticalWLS(PhysicsProcessWithoutModels)
* Scintillation(PhysicsProcessWithoutModels)
* MultipleScattering(PhysicsProcessWithoutModels)
    + __init__(self, particle)
    + content_in_adding(self)
* EMultipleScattering(PhysicsProcessWithoutModels)
    + __init__(self,particle)
    + content_in_adding(self)
* PhysicsList(ObjectWithTemplate)
    + __init__(self,physics_processes:List[PhysicsProcess])
* Cuts(ObjectWithTemplate)
    + __init__(self,volume:Volume,cuts:TV('CutT',float,Dict[Volume,float]),max_step: float=None)
* Physics(ObjectWithTemplate)
    + __init__(self, physics_list,cut_list)

simulation.py
^^^^^^^^^^^^^

* Simulation(ObjectWithTemplate)
    + __init__(self,geometry,physics,digitizers,source,paramerter,material_database=None,visualisation=None)

source.py
^^^^^^^^^

* Source(ObjectWithTemplate)
    + __init__(self,name,particle=None,activity=NOne,angle=None,shape=NOne,position:Vec3=None)
    + unified_activity(self, activity)
    + bind(self, obj)
    + is_voxelized(self)
* Particle(ObjectWithTemplate)
    + bind_source(self, source)
    + __init__(self, unstable=None, halflife=None)
* ParticlePositron(Particle)
    + __init__(self, unstalble=True,halfife=6586)
* ParticleGamma(Particle)
    + __init__(self, unstable=True,halflife=6586.2,monoenergy=511,back2back=True)
* Angular(ObjectWithTemplate)
* Shape(ObjectWithTemplate)
    + __init__(self,dimension)
* ShapePlane(Shape)
    + __init__(self)
* ShapeSurfaceOrVolume(Shape)
    + __init__(self,dimension)
* Voxelized(Shape)
    + __init__(self,read_table,read_file,reader='interfile',translator='range',positon=None)
* Cylinder(ShapeSurfaceOrVolume)
    + __init__(self,radius,halfz,dimension)
* Sphere(Shape)
    + __init__(self,radius,dimension)
* Ellipsoid(Shape)
    + __init__(self,half_sie:Vec3,dimension)
* Circle(ShapePlane)
    + __init__(slef,radius)
* Annulus(ShapePlane)
    + __init__(self,radius0,radius)
* Ellipse(ShapePlane)
    + __init__(self,half_size)
* Rectangle(ShapePlane)
    + __init__(self,half_size)
* SourceList(ObjectWithTemplate)
    + __init__(self,sources:List[Source])

utils.py
^^^^^^^^

* Vec3(ObjectWiTemplate)
    + __init__(self,x,y,z,unit=None)


predefined
-----------

__init__.py
~~~~~~~~~~~~

_cameras.py
~~~~~~~~~~~

* cylindricalPET(world: Volume, cylinder=None,rrh=None,head=None,rcb=None,block=None,rcc=None,crystal=None,lso=None,bgo=None)
* ecat(world: Volume, cylinder=None,rlb=None,rrb=None,block=None,rcc=None,crystal=None)
* opticalsystem(world: Volume,box=None,crystal=NOne,rcp=None,pixel=None)
* optical_gamma(world:Volume,crystal:VolumeLike)
* multipatchPET(world: Volume)
* optocal_surfaces(cam:Camera)

_source.py
~~~~~~~~~~

* voxelized_gamma(position,src_name='voxelized_gamma',read_table='act_range.data',read_file='act.h33')
* voxelized_F18(position,src_name='voxelized_F18',read_table='act_range.dat,read_file='act.h33')
* cylinder_source(position=Vec3(0,0,0),src_name='cylinder_source',cylinder=None,activity=NOne,particle=None,angle=None)
* plane_source(psotion=Vec3(0,0,0),src_name='plane_source',rectangle=None,activity=None,particle=None,angle=None)
* sphere_source(position=Vec3(0,0,0),src_name='sphere_source',sphere=None,activity=None,particle=None,angle=None)
* make_default_source(simu_name)
* sphere(radius,position:Vec3=Vec3(0.0,0.0,0.0,'mm'),angle:Anular=None,activity:int=1000,particle=None,name='sphere_source') -> SourceList

cameras.py
~~~~~~~~~~

digitizer.py
~~~~~~~~~~~~

* ecat_digitizer(dtvolume, rdr=None.blur=None,thres=None,uph=None,ddt=None,coin=None,coin_delay=None,coin_chain=None)
* cylindricalPET_digitizer(rdr=None,blur=NOne,thres=None,uph=None,coin=NOne,coin_delay=None)
* optical_digitizer(rdr=None)
* spect_digitizer(blur=None,spblur=None,thres=None,uph=None)


parameters.py
~~~~~~~~~~~~~
* pet_parameters(acqu=AcquisitionPeriod(),outpits=None,rand=RandomEngine(seed='auto'))
* optical_parameters(acqu=AcquisitionPrimaries(number=10000),outputs=None,rand=RandomEngineMersenneTwister(seed='auto'))
* optical_gamma(nb_primaries)

phantoms.py
~~~~~~~~~~~

* voxelized_phantom(world,image_file='phan.h33',range_file='mat_range,dat',position=None)

physics.py
~~~~~~~~~~
* pet_physics(cut_pair_list)
* optical_physics(cut_pari_list)
* gamma_physics(cut_pair_list)
* spect_physics(cut_pair_list)

simulations.py
~~~~~~~~~~~~~~

* PredefinedSimulations(Enum)
* make_default_camera(simu_name,world: Volume)
* make_default_surfaces(simu_name,cam: Camera)
* make_default_physics(simu_name,cam:Camera,phan:Phantom,cut_pair_list=None)
* make_default_digitizer(simu_name, cam: Camera)
* make_default_parameter(simu_name)
* make_simulation(simu_name,geo=None,phy=None,digi=None,src=None,para=None)
* simulation(simulation_name:PredefinedSimulations,geometry=None,physics=None,digitizer=None,source=None,parameter=None)
* optical_gamma(source=None,world_size:Vec3=Vec3(400.0,400.0,400.0,'cm'),crystal_size:Vec3=Vec3(30.0,30.0,30.0,'mm'),crystal_position:Vec3=Vec3(0.0,0.0,0.0,'mm'),crystal_material:str='LYSO',nb_prmaries=10000)

sources.py
~~~~~~~~~~


routine
-------

:ref:`routine`

 
__init__.py
~~~~~~~~~~~

analysis.py
~~~~~~~~~~~

* KEYS
* AnalysisType(Enum)
* OperationAnalysis(OperationOnfile)
    + __init(self, source_csv_filename, target_h5_filename, analysis_type:AnalysisType=None)
    + source(self,r:RoutineOnDirectory)
    + dryrun(self,r:RoutineOnDirectory)

base.py
~~~~~~~

* Operation
    + apply(self,routine)
    + dryrun(self,routine)
* Routine
    + __init__(self,operation:Tterable[Operation]=(),dryrun=False,verbose=0)
    + last_result(self)
    + work(self)
    + echo(self)
* RoutineOnDirectory(Routine)
* OperationOnFile(Operation)
    + __init__(self,filename:str)
    + target(self,r:RoutineOnDirectory) -> File
    + dryrun(self,r:RountineOnDirectory)->Dict[str,Any]
    + apply(self,r: RoutineOnDerectory) ->Dict[str,Any]
* OpeartionOnSubdirectories(Operation)
    + __init__(self,patterns:Iterable[str])
    + subdirectories(self, r: RoutineOnDirectory)
* OpeartionWithShellCall(Operation)  
    + call_args(self,r:Routine)
    + stdout(self, r:Routine)
    + run_child_program(self, r:Routine)
    + apply(self,r:Routine)
    + dryrun(self, r:Routine)->Dict[str, Iterable[str]]

cleaner.py
~~~~~~~~~~
* KEYS
* OpCleanSubdirectories(OperationOnSubdirectories)
    + apply(self, r: RoutineOnDirectory)
    + dryrun(self, r:RoutineOnDirectiory)
* OpCleanSource(Operation)
    + __init__(self,file_patterns:Iterable[str])
    + files(self, r: RoutineOnDirectory)
    + apply(self, r: RoutineInDirectory)
    + dryrun(self,r: RoutineOnDirectory)
* OpCleanFilesInAllDirectories(OperationOnSubdirectories)
    + __init__(self,file_patterns:Iterable[str],subdirectory_patterns:Iterable[str])
    + files_on_directory(self,d:Directory)   ``need to be corrected(directroy->directory)``
    + to_remove(self,r:RoutineOnDirectory)
    + apply(self,r:RoutineOnDirectory)
    + dryrun(self,r:RoutineOnDirectory)
* routine_clean(source_patterns:Iterable[str]=(),is_subdir:bool=False,dryrun:bool=False)

initialize.py
~~~~~~~~~~~~~

* KEYS
* TargetFileWithContent
    + __init__(self,target: TypeVar('FileLike',File,str).is_to_broadcast:bool=True,content:str=None)
    + to_dict(self)
    + save(self)
* OpAddToBroadcastFile(OperationOnFile)
    + __init__(self,filename)
    + apply(self,r: RoutineOnDirectory)
    + dryrun(self,r: RoutineOnDirectory)
* OpGenerateFile(OperationOnFile)
    + __init__(self,filename:str,is_to_broadcast=True)
    + content(self,r:RoutineOnDirectory) ->str
    + target_file_with_content(self,r:RoutineOnDirectory)
    + apply(self,r: RoutineOnDirectory)
    + dryrun(self,r:RoutineOnDirectory)
* OpGeneratorMac(OpGenerateFile,OpeartionWithShellCall)
    + __init__(self,script_filename:str,mac_config:str=None,mac_filename: str=None)
    + call_args(self,r: RoutineOnDirectory)
* OpgenerateMacTemplate(OpGerateFile)
    + __init__(self,filename:str,script:Script)
    + content(self,r: RoutineOnDirectory)->str
* OpGeneratorShell(OperationOnFile)
    + __init__(self,filename:str,script:Script)
    + content(self, r:RoutineOnDirectory) -> 
* OpGeneratorPhantom(OperationOnFile)
    + __init__(self,filename:str)
* OpSubdirectoriesMake(Operation)
    + __init__(self,nb_split:int,subdirectory_format:str="sub.{}")
    + apply(self, r: RoutineOnDirectory)
    + dryrun(self, r: RoutineOnDirectory)
* OpBroadcastFile(OperationONsubdirectories)
    + files_to_broadcast(self,r: RoutineOnDirectory)
    + dryrun(self,r:RoutineOnDirectory)
    + apply(self,r: RoutineOndirectory)


merger.py
~~~~~~~~~

* OpMerge(OperationOnFile,OperationOnSubdirectories)
    + __init__(self,filename:str,patterns:Iterable[str])
    + sources(self, r:RoutineOnDirectory)
    + dryrun(self,r: RoutineOnDirectory) -> JSONStr
* OpMergeWithShellCall(OpMerge,OpeartionWithShellCall)
    + __init__(self,filename:str,patterns:Iterable[str])
    + apply(self,r:RoutineOnDirectory)
    + dryrun(self,r:RoutineOnDirectory)
* OpMergeHADD(OpMergeWithShellCall)
    + call_args(self,r: RoutinOnDirectory)
* OpMergeCat(OpMergeWithShellCall)
    + call_args(self,r:RoutineOnDirectory)
* OpMergePandasConcatenate(OpMerge)
    + apply(self,r:RoutineOnDirectory)
* OpMErgeSumBinary(OpMerge)
* hadd(work_derectory:Directory,subdirectory_patterns:Iterable[str],source_filenames:Iterable[str],dryrun=False)

submit.py
~~~~~~~~~

* KEYS
* depens_from_result_dict(r: Dict[str,Any])->Iterable[int]
* append_depens_to_dict(to_submit:Dict[str,Any],previous_result: Dict[str,Any])
* parse_paths_from_dict(r: Doct[str,Any]) -> Doct[str,Any]
* submit_from_dict(r: Dct[str,Any]) -> Dict[str,Any]
* OpSubmitBroadcast(OperationOnSubdirectories,OperationOnFile)
    + __init__(self,filename,subdirectory_patterns:Iterable[str])
    + to_submit(self, r: RoutineOnDirectory) -> 'Observable[Dict[str,Any]]'
    + apply(self,r:RoutinOnDirectory) -> Dict[str,Iterable[Dict[str,str]]]
    + dryrun(self,r :RoutineOnDirectory) ->  Dict[str,Iterable[Dict[str,str]]]
* OpSubmitSingleFile(OperationOnFile)
    + __init__(self,filename:str)
    + to_submit(self, r:RoutineOnDirectory)
    + apply(self,r:RoutineOnDirectory) ->Doct[str,Any]
    + dryrunn(self,r:RoutineOnDirectory) -> Dict[str,Any]

utils.py
~~~~~~~~




scripts
-------

:ref:`scripts`


templates
^^^^^^^^^

* make_mac.j2
* post_run.j2
* run_loacal.j2
* run.j2
* sbatch.j2
* shell.j2


__init__.py
^^^^^^^^^^^

base.py
^^^^^^^

* ObjectWithTemplate(ObjectWithTemplateBase)

helper.py
^^^^^^^^^

* gate_simulation(mac_filename)
* gate_simulation_with_root_analysis(mac_filename,root_filename,analysis_c_filename) ``need to be corrected (gete->gate)``

shell.py
^^^^^^^^

* Script(ObjectWithTemplate)
    + add_task(self,task)
* Task
    + render()
* TaskWithFileArg(Task)
* GateSimulation(TaskWithFileArg)
* RootAnalysis(TaskWithFileArg)
    + __init__(self, root_filename, c_file_name)
    + render(self)
* PygateAnalysis(TaskWithFileArg)
    + __init__(self, source=NOne,target=None,output=None, name=None,analysis_type=None)
    + render(self)
* Clean(Task)
    + render(self)
* Merge(TaskWithFileArg)
* ScriptRun(Script)
    + __init__(self,work_derectory,tasks: Tuple[Task]=(),geant4_version='8.0',shell='bash',is_need_source_env=False,partition='cpu')
    + add_task(self,task)
* ScriptRunLocal(ScriptRun)
    + __init__(self,work_directory,tasks:Tuple[Task],geant4_version,shell='bash',is_nedd_source_env=False,local_work_directory=None,partition='cpu')
    + add_task(self,task)
* ScriptPostRun(Script)
    + __init__(self,tasks:Tuple[Task]=(),geant4_version='8.0',shell='bash',is_need_source_env=False,partition='cpu')
    + add_task(self,task)
* ScriptMacTemplate(ObjectWithTemplate)


test
-----

:ref:`test`


utils
-----

:ref:`utils`


__init__.py
^^^^^^^^^^^^

object_with_template.py
^^^^^^^^^^^^^^^^^^^^^^^

* EnvironmentOfPackage
    + __init__(self,pkg_name)
    + get_or_create_env(self)
* default_suffix(s: str, suffix: str, is_auto_add_point_prefix=True)
* ObjectWithTemplateBase
    + template_name(self)
    + render(self)

strs.py
^^^^^^^

syscall.py
^^^^^^^^^^

* shell_call(commands: Iterable[str] or str, is_echo=True)


typing.py
^^^^^^^^^

* JSONStr(str)


__init__.py
-----------

cleaner.py
-----------

* Cleaner
    + __init__(self,fs,config)
    + clean(self)
    + msg(self,path)
    + _clean_subs(self)
    + _clean_sources(self)

conf.py
--------

* KEYS
* SUBMIT_KEYS
* CLEAN_KEYS
* ANALYSIS_KEYS
* INIT_KEYS
    + BROADCAST_KEYS
    + EXTERNAL_KEYS
    + MAC_KEYS
    + SHELL_KEYS
* PHANTOM_KEYS

config_maker.py
---------------

* ConfigMaker
    + _make_pygate_config(cls,fs,target,congfig_filename=None)
    + _make_mac_config(cls,fs,target,config=None,mac_config=None)
    + make(cls, fs,target,pygate_config=None,mac_config=None)

config.py
---------

configs.py
-----------

initializer.py
--------------

* Initializer
    + __init__(self,fs,config)
    + _copy_sources_from_template(self)
    + _make_mac(self)
    + _make_phantom(self)
    + _sub_dir_name(self,i)
    + _nb_sub_dirs(self)
    + _make_subdirs(self)
    + _make_map_shell_scripts(self)
    + _copy_sources_to_subdirs(self)
    + pre_sub(self)
    + make_sub(self)

merger.py
----------

* Merger
    + __init__(self,fs,config)
    + _path_of_file_in_sub_dirs(self,base_filename)
    + msg(self,method,target,sources)
    + _hadd(self,task)
    + _cat(self,task)
    + _sum(self,task)
    + _copy(self,task)
    + merge(self)

phantom.py
----------

* PhantomBinFileMaker:
    + __init__(self,fs,phantom_files)
    + _load_data(self,source)
    + _make_bin(self,target,data)
    + make(self)

renderable.py
-------------

* Renderable
    + render(self) ->str

service.py
----------

* make_config(target='.')
* init(config,method)
* submit(config)
* merge(config)
* clean(config)

shell.py
--------

* ShellScriptBase
    + __init__(self,fs,workdir:str, output:str,tasks:list,shell='zsh',version='7.2')
    + _add_if_gate(self,task)
    + _add_if_root(self,task)
    + _get_workdir_on_local_and_server(self)
    + _make(self)
* ShellScriptMerge(ShellScriptBase)
    + __init__(self,fs,workdir:str,output:str,tasks:list,shell='zsh')
    + _make(self)
* ShellScriptMaker
    + __init__(self,fs,config)
    + make(self)

submitter.py
-------------

* Submitter
    + __init__(self,fs,config)
    + _get_map_info(self)
    + _get_merge_info(self)
    + submit(self)
    + _echo(self,info,fout)
    + _slurm(self, run_infos,post_infos)
    + _hqlf(self,run_infos,post_infos)

utils.py
--------

* get_scripts_path
* load_script(name)
* sub_dir_filters(config)

