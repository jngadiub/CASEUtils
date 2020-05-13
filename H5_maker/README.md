#H5 Maker

Make h5's from the extended NanoAOD (pancakes) after applying a preselection. 

The preselection is:

Filters: 
Flag\_goodVertices, Flag\_globalTightHalo2016Filter, Flag\_eeBadScFilter, Flag\_HBHENoiseFilter, Flag\_HBHENoiseIsoFilter, Flag\_ecalBadCalibFilter, Flag\_EcalDeadCellTriggerPrimitiveFilter, Flag\_BadChargedCandidateFilter

Triggers:
2016: HLT\_PFHT800, HLT\_PFHT900, HLT\_PFJet450, HLT\_PFJet500, HLT\_AK8PFJet450, HLT\_AK8PFJet500
2017/8: HLT\_PFHT1050, HLT\_PFJet500, HLT\_AK8PFJet380\_TrimMass30, HLT\_AK8PFJet400\_TrimMass30

Mjj > 1200.

2 AK8 Jets with tight ID,  pt > 200 , |eta| < 2.5


The output is an h5 dataset with several different keys
In general the highest two pt jets are the dijet candidate.
The jets are labeled so that 'j1' is the more massive jet in the event and 'j2'
the less massive jet


The data in each keys are:


preselection\_eff: 
truth\_label :  single int. Labels  the type of event. 0 is QCD, signals are => 1 (depends on dataset), other backgrounds are TBD but will be < 0
event\_info: 6 floats. [eventNum, MET, MET\_phi, genWeight, leptonic\_decay]
leptonic decay is a flag (current not set!) that will check the generator level
decay to see if it is leptonic, semi-leptonic or full hadronic
jet\_kinematics:  14 floats. Mjj, delta\_eta (between j1 and j2), followed by the 4 vectors of j1, j2 and j3  in pt,eta,phi,m\_softdrop format (if no 3rd jet passing cuts, zeros)
j1(2)\_extraInfo :  7 floats. 4 nsubjettiness scores (tau\_i), followed by LSF3,
btag score (max deepB score of ak4 subjets) and number of PF constituents
j1(2)\_PFCands: 4 vectors of up to 100 PFCands in  Px, Py, Pz, E  format. Zero
padded


H5\_merge.py is also useful. It combines different h5 files together like hadd.
Does a weighted average for preselection\_eff