"CREATE CONSTRAINT action_id_unique FOR (node:Action) REQUIRE (node.action_id) IS UNIQUE;
CREATE CONSTRAINT anatomy_id_unique FOR (node:Anatomical) REQUIRE (node.anatomy_id) IS UNIQUE;
CREATE CONSTRAINT arbitration_id_unique FOR (node:Arbitration) REQUIRE (node.arbitration_id) IS UNIQUE;
CREATE CONSTRAINT artifact_id_unique FOR (node:Artifact) REQUIRE (node.artifact_id) IS UNIQUE;
CREATE CONSTRAINT case_id_unique FOR (node:Case) REQUIRE (node.case_id) IS UNIQUE;
CREATE CONSTRAINT component_id_unique FOR (node:LearningComponentNode) REQUIRE (node.component_id) IS UNIQUE;
CREATE CONSTRAINT cpt_code_unique FOR (node:CPTCode) REQUIRE (node.cpt_code) IS UNIQUE;
CREATE CONSTRAINT diagnosis_id_unique FOR (node:Diagnosis) REQUIRE (node.diagnosis_id) IS UNIQUE;
CREATE CONSTRAINT finding_id_unique FOR (node:Finding) REQUIRE (node.finding_id) IS UNIQUE;
CREATE CONSTRAINT icd_code_unique FOR (node:ICDCode) REQUIRE (node.icd_code) IS UNIQUE;
CREATE CONSTRAINT intent_id_unique FOR (node:ClinicalIntent) REQUIRE (node.intent_id) IS UNIQUE;
CREATE CONSTRAINT learning_node_id_unique FOR (node:LearningNode_CASE) REQUIRE (node.learning_node_id) IS UNIQUE;
CREATE CONSTRAINT procedure_id_unique FOR (node:Procedure) REQUIRE (node.procedure_id) IS UNIQUE;
CREATE CONSTRAINT provenance_id_unique FOR (node:Provenance) REQUIRE (node.event_id) IS UNIQUE;
CREATE CONSTRAINT snapshot_id_unique FOR (node:GraphSnapshotNode) REQUIRE (node.graph_snapshot_id) IS UNIQUE;
CREATE CONSTRAINT UNIQUE_IMPORT_NAME FOR (node:`UNIQUE IMPORT LABEL`) REQUIRE (node.`UNIQUE IMPORT ID`) IS UNIQUE;
UNWIND [{_id:40, properties:{bundle_type:"idr_submission", created_timestamp:"2026-05-15T08:45:00Z", evidence_bundle_id:"EVID-BUNDLE-001"}}] AS row
CREATE (n:`UNIQUE IMPORT LABEL`{`UNIQUE IMPORT ID`: row._id}) SET n += row.properties SET n:EvidenceBundleNode;
UNWIND [{_id:43, properties:{stage_timestamp:"2026-05-15T09:32:00Z", stage_name:"clinical_truth_assembly", rail_stage_id:"RAIL-STAGE-001", stage_status:"validated"}}, {_id:45, properties:{validation_result:"no_repair_needed", stage_timestamp:"2026-05-15T09:45:00Z", stage_name:"validation_and_repair", rail_stage_id:"RAIL-STAGE-002", stage_status:"repair_complete", repair_loop_count:0}}] AS row
CREATE (n:`UNIQUE IMPORT LABEL`{`UNIQUE IMPORT ID`: row._id}) SET n += row.properties SET n:RailStageNode;
UNWIND [{intent_id:"INTENT-BCT-001", properties:{intent_type:"therapeutic_strategy", intent_context:"Stage I-II disease, patient preference for conservation", intent_label:"Breast conserving therapy with sentinel node biopsy", created_timestamp:"2026-03-12T09:15:00Z"}}] AS row
CREATE (n:ClinicalIntent{intent_id: row.intent_id}) SET n += row.properties;
UNWIND [{_id:39, properties:{submission_timestamp:"2026-05-15T09:00:00Z", submission_packet_id:"SUBPACK-ARB-001", payer:"UnitedHealthcare", status:"submitted"}}] AS row
CREATE (n:`UNIQUE IMPORT LABEL`{`UNIQUE IMPORT ID`: row._id}) SET n += row.properties SET n:SubmissionPacketNode;
UNWIND [{artifact_id:"ART-OPNOTE-001", properties:{artifact_type:"operative_report", generation_timestamp:"2026-04-16T10:30:00Z", artifact_status:"draft"}}, {artifact_id:"ART-IDR-BUNDLE-001", properties:{artifact_type:"idr_submission_bundle", generation_timestamp:"2026-05-15T09:00:00Z", artifact_status:"prepared"}}] AS row
CREATE (n:Artifact{artifact_id: row.artifact_id}) SET n += row.properties;
UNWIND [{arbitration_id:"ARB-001-2026", properties:{submission_date:"2026-05-10", cooling_off_period:"30 days", resolution_date:"2026-08-01", case_status:"resolved", resolution_notes:"Payer agreed to full reimbursement after review of operative report, codes, and flap viability finding", payer:"UnitedHealthcare"}}] AS row
CREATE (n:Arbitration{arbitration_id: row.arbitration_id}) SET n += row.properties;
UNWIND [{diagnosis_id:"DX-001", properties:{icd_code:"C50.411", diagnosis_label:"Invasive ductal carcinoma of right breast", diagnosis_status:"postoperative_confirmed"}}] AS row
CREATE (n:Diagnosis{diagnosis_id: row.diagnosis_id}) SET n += row.properties;
UNWIND [{learning_node_id:"LEARN-CASE-2026-001", properties:{creation_timestamp:"2026-03-18T13:30:00Z", learning_version:"v1.5.1"}}] AS row
CREATE (n:LearningNode_CASE{learning_node_id: row.learning_node_id}) SET n += row.properties;
UNWIND [{event_id:"PROV-ART-GEN-001", properties:{actor:"SEF-System-v1.0", event_type:"artifact_generation", system_state:"draft_mode", timestamp:"2026-04-16T10:30:00Z"}}, {event_id:"PROV-STATUS-UPDATE-001", properties:{actor:"SURG-456", event_type:"diagnosis_status_update", notes:"Reviewed pathology report; confirmed clear margins and updated status", system_state:"postop_review_complete", timestamp:"2026-04-21T08:45:00Z"}}, {event_id:"PROV-IDR-PREP-001", properties:{actor:"BILLING-SPEC-789", event_type:"artifact_preparation", notes:"Compiled operative report, codes, and arbitration details for UHC dispute", system_state:"pre-submission_review", timestamp:"2026-05-15T09:00:00Z"}}, {event_id:"PROV-RECON-DOC-001", properties:{actor:"SURG-456", event_type:"procedure_documentation", notes:"Dictated operative note for DIEP flap reconstruction; confirmed microvascular patency", system_state:"postop_documentation", timestamp:"2026-07-16T11:00:00Z"}}, {event_id:"PROV-ARB-RES-001", properties:{actor:"SEF-Billing-Team", event_type:"arbitration_resolution", notes:"UHC reversed initial denial; all CPTs paid based on comprehensive evidence chain", system_state:"resolved_full_payment", timestamp:"2026-08-01T14:00:00Z"}}] AS row
CREATE (n:Provenance{event_id: row.event_id}) SET n += row.properties;
UNWIND [{anatomy_id:"ANAT-AXILLA-R", properties:{ontology_reference:"SNOMED:48543004", region:"axilla", laterality:"right", anatomic_label:"Right axillary lymph nodes"}}, {anatomy_id:"ANAT-BREAST-R-UOQ", properties:{ontology_reference:"SNOMED:76752008", region:"upper_outer_quadrant", laterality:"right", anatomic_label:"Right breast upper outer quadrant"}}, {anatomy_id:"ANAT-ABDOMEN", properties:{ontology_reference:"SNOMED:69830009", region:"abdomen", laterality:"bilateral", anatomic_label:"Lower abdomen (DIEP donor site)"}}, {anatomy_id:"ANAT-ABDOMEN-LOWER", properties:{ontology_reference:"SNOMED:69830009", region:"abdomen", laterality:"bilateral", anatomic_label:"Lower abdominal wall (DIEP donor site)"}}] AS row
CREATE (n:Anatomical{anatomy_id: row.anatomy_id}) SET n += row.properties;
UNWIND [{component_id:"COMP-001", properties:{node_type:"Finding", payload_json:"{\"finding_id\":\"FIND-PREOP-001\",\"finding_label\":\"2 cm palpable mass in upper outer quadrant\",\"clinical_phase\":\"preoperative\",\"semantic_summary\":\"Preoperative clinical discovery supporting invasive ductal carcinoma diagnosis\"}", provenance_json:"{\"provider_id\":\"SURG-456\",\"facility\":\"HOSP-OC-01\",\"timestamp\":\"2026-03-10T14:30:00Z\"}"}}, {component_id:"COMP-DX-001", properties:{node_type:"Diagnosis", payload_json:"{\"diagnosis_id\":\"DX-001\",\"diagnosis_label\":\"Invasive ductal carcinoma of right breast\",\"diagnosis_status\":\"postoperative_confirmed\",\"icd_code\":\"C50.411\"}", provenance_json:"{\"provider_id\":\"SURG-456\",\"facility\":\"HOSP-OC-01\",\"timestamp\":\"2026-04-20T14:15:00Z\"}"}}, {component_id:"COMP-PROC-001", properties:{node_type:"Procedure", payload_json:"{\"procedure_id\":\"PROC-001\",\"procedure_label\":\"Partial mastectomy with sentinel lymph node biopsy\",\"procedure_role\":\"primary\"}", provenance_json:"{\"provider_id\":\"SURG-456\",\"facility\":\"HOSP-OC-01\",\"timestamp\":\"2026-04-15T08:45:00Z\"}"}}, {component_id:"COMP-ACT-001", properties:{node_type:"Action", payload_json:"{\"action_id\":\"ACT-EXC-001\",\"action_label\":\"Wide local excision of primary tumor\",\"procedural_domain\":\"oncologic_excision\"}", provenance_json:"{\"provider_id\":\"SURG-456\",\"facility\":\"HOSP-OC-01\",\"timestamp\":\"2026-04-15T08:45:00Z\"}"}}, {component_id:"COMP-CPT-001", properties:{node_type:"CPTCode", payload_json:"{\"cpt_code\":\"19301\",\"cpt_label\":\"Mastectomy, partial\",\"unit_count\":1}", provenance_json:"{\"provider_id\":\"SURG-456\",\"facility\":\"HOSP-OC-01\",\"timestamp\":\"2026-04-15T08:45:00Z\"}"}}, {component_id:"COMP-ART-001", properties:{node_type:"Artifact", payload_json:"{\"artifact_id\":\"ART-OPNOTE-001\",\"artifact_type\":\"operative_report\",\"artifact_status\":\"draft\"}", provenance_json:"{\"provider_id\":\"SURG-456\",\"facility\":\"HOSP-OC-01\",\"timestamp\":\"2026-04-16T10:30:00Z\"}"}}] AS row
CREATE (n:LearningComponentNode{component_id: row.component_id}) SET n += row.properties;
UNWIND [{_id:42, properties:{rail_execution_id:"RAIL-EXEC-001", execution_status:"completed", rail_version:"PRS-v1.5.1", execution_timestamp:"2026-05-15T09:30:00Z"}}] AS row
CREATE (n:`UNIQUE IMPORT LABEL`{`UNIQUE IMPORT ID`: row._id}) SET n += row.properties SET n:RailExecutionNode;
UNWIND [{finding_id:"FIND-PREOP-001", properties:{clinical_phase:"preoperative", finding_label:"2 cm palpable mass in upper outer quadrant", source_document:"clinic_note_2026-03-10.pdf", finding_type:"preoperative", finding_class:"clinical_exam", timestamp:"2026-03-10T14:30:00Z"}}, {finding_id:"FIND-POSTOP-001", properties:{clinical_phase:"postoperative", finding_label:"Pathology confirms clear margins, no residual tumor", source_document:"pathology_report_2026-04-20.pdf", finding_type:"postoperative", finding_class:"pathology_report", timestamp:"2026-04-20T11:00:00Z"}}, {finding_id:"FIND-POSTOP-PATH-001", properties:{clinical_phase:"postoperative", finding_label:"Pathology: invasive ductal carcinoma, clear margins (2 mm), no LVI", source_document:"path_report_2026-04-20.pdf", finding_type:"postoperative", finding_class:"pathology", timestamp:"2026-04-20T14:15:00Z"}}, {finding_id:"FIND-INTRA-001", properties:{clinical_phase:"intraoperative", finding_label:"Intraoperative frozen section: negative for residual tumor at margins", source_document:"intraop_frozen_section_2026-04-15.pdf", finding_type:"intraoperative", finding_class:"frozen_section_pathology", timestamp:"2026-04-15T10:15:00Z"}}, {finding_id:"FIND-INTRA-RECON-001", properties:{clinical_phase:"intraoperative", finding_label:"Intraoperative indocyanine green angiography confirms excellent flap perfusion and no venous congestion", source_document:"intraop_icg_angiography_2026-07-15.pdf", finding_type:"intraoperative", finding_class:"angiography_assessment", timestamp:"2026-07-15T10:30:00Z"}}] AS row
CREATE (n:Finding{finding_id: row.finding_id}) SET n += row.properties;
UNWIND [{action_id:"ACT-SLNB-001", properties:{action_class:"biopsy", execution_context:"intraoperative", procedural_domain:"staging", action_label:"Sentinel lymph node mapping and biopsy", timestamp:"2026-04-15T09:20:00Z", anatomic_target:"axillary lymph nodes"}}, {action_id:"ACT-EXC-001", properties:{action_class:"excision", execution_context:"intraoperative", procedural_domain:"oncologic_excision", action_label:"Wide local excision of primary tumor", timestamp:"2026-04-15T08:45:00Z", anatomic_target:"breast mass"}}, {action_id:"ACT-DIEP-001", properties:{action_class:"microvascular_flap", execution_context:"intraoperative", procedural_domain:"reconstructive_transfer", action_label:"DIEP flap harvest from abdomen with microvascular anastomosis to internal mammary vessels", timestamp:"2026-07-15T08:00:00Z", anatomic_target:"abdomen to right breast"}}] AS row
CREATE (n:Action{action_id: row.action_id}) SET n += row.properties;
UNWIND [{case_id:"CASE-2026-001", properties:{patient_id:"PT-987654", surgeon_id:"SURG-456", facility_id:"HOSP-OC-01", procedure_date:"2026-04-15", specialty_modules_loaded:["Breast", "Oncologic"], case_context:"Breast oncology referral"}}] AS row
CREATE (n:Case{case_id: row.case_id}) SET n += row.properties;
UNWIND [{graph_snapshot_id:"SNAP-2026-03-18-001", properties:{case_reference:"CASE-2026-001", module_version_bindings:["Clinical-v1.5", "Billing-v1.2", "Arbitration-v1.3"], snapshot_timestamp:"2026-03-18T13:00:00Z", ontology_versions:["SEF-v1.5.1", "ActionOntology-v2.1", "DiagnosisOntology-v3.0"], rail_version:"PRS-v1.5.1"}}] AS row
CREATE (n:GraphSnapshotNode{graph_snapshot_id: row.graph_snapshot_id}) SET n += row.properties;
UNWIND [{cpt_code:"19301", properties:{cpt_label:"Mastectomy, partial (e.g., lumpectomy, tylectomy, quadrantectomy, segmentectomy)", domain:"breast", unit_count:1}}, {cpt_code:"38525", properties:{cpt_label:"Biopsy or excision of lymph node(s); open, deep axillary node(s)", domain:"lymph_node", unit_count:1}}, {cpt_code:"38900", properties:{cpt_label:"Intraoperative identification (e.g., mapping) of sentinel lymph node(s)", domain:"intraoperative_mapping", unit_count:1}}, {cpt_code:"19364", properties:{cpt_label:"Breast reconstruction with free flap (microvascular)", domain:"reconstruction", unit_count:1}}] AS row
CREATE (n:CPTCode{cpt_code: row.cpt_code}) SET n += row.properties;
UNWIND [{icd_code:"C50.411", properties:{coding_version:"ICD-10-CM 2026", icd_label:"Malignant neoplasm of upper-outer quadrant of right female breast"}}, {icd_code:"E11.9", properties:{coding_version:"ICD-10-CM 2026", icd_label:"Type 2 diabetes mellitus without complications"}}, {icd_code:"Z90.13", properties:{coding_version:"ICD-10-CM 2026", icd_label:"Acquired absence of bilateral breasts and nipples"}}] AS row
CREATE (n:ICDCode{icd_code: row.icd_code}) SET n += row.properties;
UNWIND [{procedure_id:"PROC-001", properties:{procedure_label:"Partial mastectomy with sentinel lymph node biopsy", procedure_role:"primary", procedure_species:"management_driven", execution_context:"elective", timestamp:"2026-04-15"}}, {procedure_id:"PROC-RECON-001", properties:{procedure_label:"Delayed deep inferior epigastric perforator (DIEP) flap breast reconstruction", procedure_role:"secondary", procedure_species:"management_driven", execution_context:"elective", timestamp:"2026-07-15"}}] AS row
CREATE (n:Procedure{procedure_id: row.procedure_id}) SET n += row.properties;
UNWIND [{start: {component_id:"COMP-001"}, end: {learning_node_id:"LEARN-CASE-2026-001"}, properties:{}}, {start: {component_id:"COMP-DX-001"}, end: {learning_node_id:"LEARN-CASE-2026-001"}, properties:{}}] AS row
MATCH (start:LearningComponentNode{component_id: row.start.component_id})
MATCH (end:LearningNode_CASE{learning_node_id: row.end.learning_node_id})
CREATE (start)-[r:PART_OF]->(end) SET r += row.properties;
UNWIND [{start: {_id:43}, end: {_id:42}, properties:{}}, {start: {_id:45}, end: {_id:42}, properties:{}}] AS row
MATCH (start:`UNIQUE IMPORT LABEL`{`UNIQUE IMPORT ID`: row.start._id})
MATCH (end:`UNIQUE IMPORT LABEL`{`UNIQUE IMPORT ID`: row.end._id})
CREATE (start)-[r:PART_OF_EXECUTION]->(end) SET r += row.properties;
UNWIND [{start: {_id:42}, end: {_id:39}, properties:{}}] AS row
MATCH (start:`UNIQUE IMPORT LABEL`{`UNIQUE IMPORT ID`: row.start._id})
MATCH (end:`UNIQUE IMPORT LABEL`{`UNIQUE IMPORT ID`: row.end._id})
CREATE (start)-[r:PRODUCES]->(end) SET r += row.properties;
UNWIND [{start: {_id:39}, end: {arbitration_id:"ARB-001-2026"}, properties:{}}] AS row
MATCH (start:`UNIQUE IMPORT LABEL`{`UNIQUE IMPORT ID`: row.start._id})
MATCH (end:Arbitration{arbitration_id: row.end.arbitration_id})
CREATE (start)-[r:REFERENCES]->(end) SET r += row.properties;
UNWIND [{start: {intent_id:"INTENT-BCT-001"}, end: {procedure_id:"PROC-001"}, properties:{}}] AS row
MATCH (start:ClinicalIntent{intent_id: row.start.intent_id})
MATCH (end:Procedure{procedure_id: row.end.procedure_id})
CREATE (start)-[r:ANTICIPATES]->(end) SET r += row.properties;
UNWIND [{start: {action_id:"ACT-SLNB-001"}, end: {anatomy_id:"ANAT-AXILLA-R"}, properties:{}}, {start: {action_id:"ACT-EXC-001"}, end: {anatomy_id:"ANAT-BREAST-R-UOQ"}, properties:{}}, {start: {action_id:"ACT-DIEP-001"}, end: {anatomy_id:"ANAT-ABDOMEN-LOWER"}, properties:{}}] AS row
MATCH (start:Action{action_id: row.start.action_id})
MATCH (end:Anatomical{anatomy_id: row.end.anatomy_id})
CREATE (start)-[r:PERFORMED_ON]->(end) SET r += row.properties;
UNWIND [{start: {artifact_id:"ART-IDR-BUNDLE-001"}, end: {artifact_id:"ART-OPNOTE-001"}, properties:{}}] AS row
MATCH (start:Artifact{artifact_id: row.start.artifact_id})
MATCH (end:Artifact{artifact_id: row.end.artifact_id})
CREATE (start)-[r:SUPPORTED_BY]->(end) SET r += row.properties;
UNWIND [{start: {event_id:"PROV-ART-GEN-001"}, end: {artifact_id:"ART-OPNOTE-001"}, properties:{}}, {start: {event_id:"PROV-IDR-PREP-001"}, end: {artifact_id:"ART-IDR-BUNDLE-001"}, properties:{}}, {start: {event_id:"PROV-ARB-RES-001"}, end: {artifact_id:"ART-IDR-BUNDLE-001"}, properties:{}}] AS row
MATCH (start:Provenance{event_id: row.start.event_id})
MATCH (end:Artifact{artifact_id: row.end.artifact_id})
CREATE (start)-[r:RECORDED_FOR]->(end) SET r += row.properties;
UNWIND [{start: {_id:43}, end: {graph_snapshot_id:"SNAP-2026-03-18-001"}, properties:{}}, {start: {_id:45}, end: {graph_snapshot_id:"SNAP-2026-03-18-001"}, properties:{}}] AS row
MATCH (start:`UNIQUE IMPORT LABEL`{`UNIQUE IMPORT ID`: row.start._id})
MATCH (end:GraphSnapshotNode{graph_snapshot_id: row.end.graph_snapshot_id})
CREATE (start)-[r:VALIDATES_SNAPSHOT]->(end) SET r += row.properties;
UNWIND [{start: {finding_id:"FIND-INTRA-001"}, end: {action_id:"ACT-EXC-001"}, properties:{}}, {start: {finding_id:"FIND-INTRA-RECON-001"}, end: {action_id:"ACT-DIEP-001"}, properties:{}}] AS row
MATCH (start:Finding{finding_id: row.start.finding_id})
MATCH (end:Action{action_id: row.end.action_id})
CREATE (start)-[r:SUPPORTED_BY]->(end) SET r += row.properties;
UNWIND [{start: {learning_node_id:"LEARN-CASE-2026-001"}, end: {case_id:"CASE-2026-001"}, properties:{}}] AS row
MATCH (start:LearningNode_CASE{learning_node_id: row.start.learning_node_id})
MATCH (end:Case{case_id: row.end.case_id})
CREATE (start)-[r:BELONGS_TO]->(end) SET r += row.properties;
UNWIND [{start: {arbitration_id:"ARB-001-2026"}, end: {artifact_id:"ART-OPNOTE-001"}, properties:{}}] AS row
MATCH (start:Arbitration{arbitration_id: row.start.arbitration_id})
MATCH (end:Artifact{artifact_id: row.end.artifact_id})
CREATE (start)-[r:SUBMITTED_WITH]->(end) SET r += row.properties;
UNWIND [{start: {procedure_id:"PROC-001"}, end: {cpt_code:"19301"}, properties:{}}, {start: {procedure_id:"PROC-001"}, end: {cpt_code:"38525"}, properties:{}}, {start: {procedure_id:"PROC-001"}, end: {cpt_code:"38900"}, properties:{}}, {start: {procedure_id:"PROC-RECON-001"}, end: {cpt_code:"19364"}, properties:{}}] AS row
MATCH (start:Procedure{procedure_id: row.start.procedure_id})
MATCH (end:CPTCode{cpt_code: row.end.cpt_code})
CREATE (start)-[r:MAPS_TO]->(end) SET r += row.properties;
UNWIND [{start: {event_id:"PROV-ART-GEN-001"}, end: {case_id:"CASE-2026-001"}, properties:{}}, {start: {event_id:"PROV-STATUS-UPDATE-001"}, end: {case_id:"CASE-2026-001"}, properties:{}}, {start: {event_id:"PROV-IDR-PREP-001"}, end: {case_id:"CASE-2026-001"}, properties:{}}, {start: {event_id:"PROV-RECON-DOC-001"}, end: {case_id:"CASE-2026-001"}, properties:{}}, {start: {event_id:"PROV-ARB-RES-001"}, end: {case_id:"CASE-2026-001"}, properties:{}}] AS row
MATCH (start:Provenance{event_id: row.start.event_id})
MATCH (end:Case{case_id: row.end.case_id})
CREATE (start)-[r:RECORDED_FOR]->(end) SET r += row.properties;
UNWIND [{start: {event_id:"PROV-RECON-DOC-001"}, end: {action_id:"ACT-DIEP-001"}, properties:{}}] AS row
MATCH (start:Provenance{event_id: row.start.event_id})
MATCH (end:Action{action_id: row.end.action_id})
CREATE (start)-[r:RECORDED_FOR]->(end) SET r += row.properties;
UNWIND [{start: {case_id:"CASE-2026-001"}, end: {finding_id:"FIND-PREOP-001"}, properties:{}}, {start: {case_id:"CASE-2026-001"}, end: {finding_id:"FIND-POSTOP-001"}, properties:{}}, {start: {case_id:"CASE-2026-001"}, end: {finding_id:"FIND-POSTOP-PATH-001"}, properties:{}}, {start: {case_id:"CASE-2026-001"}, end: {finding_id:"FIND-INTRA-001"}, properties:{}}, {start: {case_id:"CASE-2026-001"}, end: {finding_id:"FIND-INTRA-RECON-001"}, properties:{}}] AS row
MATCH (start:Case{case_id: row.start.case_id})
MATCH (end:Finding{finding_id: row.end.finding_id})
CREATE (start)-[r:HAS_FINDING]->(end) SET r += row.properties;
UNWIND [{start: {event_id:"PROV-IDR-PREP-001"}, end: {arbitration_id:"ARB-001-2026"}, properties:{}}, {start: {event_id:"PROV-ARB-RES-001"}, end: {arbitration_id:"ARB-001-2026"}, properties:{}}] AS row
MATCH (start:Provenance{event_id: row.start.event_id})
MATCH (end:Arbitration{arbitration_id: row.end.arbitration_id})
CREATE (start)-[r:RECORDED_FOR]->(end) SET r += row.properties;
UNWIND [{start: {finding_id:"FIND-PREOP-001"}, end: {anatomy_id:"ANAT-BREAST-R-UOQ"}, properties:{}}, {start: {finding_id:"FIND-POSTOP-001"}, end: {anatomy_id:"ANAT-BREAST-R-UOQ"}, properties:{}}, {start: {finding_id:"FIND-POSTOP-PATH-001"}, end: {anatomy_id:"ANAT-BREAST-R-UOQ"}, properties:{}}, {start: {finding_id:"FIND-INTRA-001"}, end: {anatomy_id:"ANAT-BREAST-R-UOQ"}, properties:{}}, {start: {finding_id:"FIND-INTRA-RECON-001"}, end: {anatomy_id:"ANAT-ABDOMEN-LOWER"}, properties:{}}] AS row
MATCH (start:Finding{finding_id: row.start.finding_id})
MATCH (end:Anatomical{anatomy_id: row.end.anatomy_id})
CREATE (start)-[r:LOCATED_IN]->(end) SET r += row.properties;
UNWIND [{start: {artifact_id:"ART-OPNOTE-001"}, end: {procedure_id:"PROC-001"}, properties:{}}] AS row
MATCH (start:Artifact{artifact_id: row.start.artifact_id})
MATCH (end:Procedure{procedure_id: row.end.procedure_id})
CREATE (start)-[r:SUPPORTED_BY]->(end) SET r += row.properties;
UNWIND [{start: {case_id:"CASE-2026-001"}, end: {procedure_id:"PROC-RECON-001"}, properties:{}}] AS row
MATCH (start:Case{case_id: row.start.case_id})
MATCH (end:Procedure{procedure_id: row.end.procedure_id})
CREATE (start)-[r:HAS_PROCEDURE]->(end) SET r += row.properties;
UNWIND [{start: {case_id:"CASE-2026-001"}, end: {artifact_id:"ART-OPNOTE-001"}, properties:{}}, {start: {case_id:"CASE-2026-001"}, end: {artifact_id:"ART-IDR-BUNDLE-001"}, properties:{}}] AS row
MATCH (start:Case{case_id: row.start.case_id})
MATCH (end:Artifact{artifact_id: row.end.artifact_id})
CREATE (start)-[r:GENERATES]->(end) SET r += row.properties;
UNWIND [{start: {diagnosis_id:"DX-001"}, end: {intent_id:"INTENT-BCT-001"}, properties:{}}] AS row
MATCH (start:Diagnosis{diagnosis_id: row.start.diagnosis_id})
MATCH (end:ClinicalIntent{intent_id: row.end.intent_id})
CREATE (start)-[r:GENERATES_INTENT]->(end) SET r += row.properties;
UNWIND [{start: {diagnosis_id:"DX-001"}, end: {icd_code:"C50.411"}, properties:{}}, {start: {diagnosis_id:"DX-001"}, end: {icd_code:"E11.9"}, properties:{}}, {start: {diagnosis_id:"DX-001"}, end: {icd_code:"Z90.13"}, properties:{}}] AS row
MATCH (start:Diagnosis{diagnosis_id: row.start.diagnosis_id})
MATCH (end:ICDCode{icd_code: row.end.icd_code})
CREATE (start)-[r:MAPS_TO]->(end) SET r += row.properties;
UNWIND [{start: {_id:39}, end: {case_id:"CASE-2026-001"}, properties:{}}] AS row
MATCH (start:`UNIQUE IMPORT LABEL`{`UNIQUE IMPORT ID`: row.start._id})
MATCH (end:Case{case_id: row.end.case_id})
CREATE (start)-[r:SUBMITTED_FOR]->(end) SET r += row.properties;
UNWIND [{start: {arbitration_id:"ARB-001-2026"}, end: {icd_code:"C50.411"}, properties:{}}] AS row
MATCH (start:Arbitration{arbitration_id: row.start.arbitration_id})
MATCH (end:ICDCode{icd_code: row.end.icd_code})
CREATE (start)-[r:REFERENCES]->(end) SET r += row.properties;
UNWIND [{start: {_id:42}, end: {case_id:"CASE-2026-001"}, properties:{}}] AS row
MATCH (start:`UNIQUE IMPORT LABEL`{`UNIQUE IMPORT ID`: row.start._id})
MATCH (end:Case{case_id: row.end.case_id})
CREATE (start)-[r:EXECUTES]->(end) SET r += row.properties;
UNWIND [{start: {action_id:"ACT-DIEP-001"}, end: {finding_id:"FIND-INTRA-RECON-001"}, properties:{}}] AS row
MATCH (start:Action{action_id: row.start.action_id})
MATCH (end:Finding{finding_id: row.end.finding_id})
CREATE (start)-[r:SUPPORTED_BY]->(end) SET r += row.properties;
UNWIND [{start: {component_id:"COMP-001"}, end: {graph_snapshot_id:"SNAP-2026-03-18-001"}, properties:{}}, {start: {component_id:"COMP-DX-001"}, end: {graph_snapshot_id:"SNAP-2026-03-18-001"}, properties:{}}] AS row
MATCH (start:LearningComponentNode{component_id: row.start.component_id})
MATCH (end:GraphSnapshotNode{graph_snapshot_id: row.end.graph_snapshot_id})
CREATE (start)-[r:DERIVED_FROM]->(end) SET r += row.properties;
UNWIND [{start: {_id:40}, end: {artifact_id:"ART-IDR-BUNDLE-001"}, properties:{}}] AS row
MATCH (start:`UNIQUE IMPORT LABEL`{`UNIQUE IMPORT ID`: row.start._id})
MATCH (end:Artifact{artifact_id: row.end.artifact_id})
CREATE (start)-[r:INCLUDES]->(end) SET r += row.properties;
UNWIND [{start: {event_id:"PROV-STATUS-UPDATE-001"}, end: {diagnosis_id:"DX-001"}, properties:{}}] AS row
MATCH (start:Provenance{event_id: row.start.event_id})
MATCH (end:Diagnosis{diagnosis_id: row.end.diagnosis_id})
CREATE (start)-[r:RECORDED_FOR]->(end) SET r += row.properties;
UNWIND [{start: {artifact_id:"ART-OPNOTE-001"}, end: {icd_code:"C50.411"}, properties:{}}, {start: {artifact_id:"ART-OPNOTE-001"}, end: {icd_code:"E11.9"}, properties:{}}, {start: {artifact_id:"ART-OPNOTE-001"}, end: {icd_code:"Z90.13"}, properties:{}}, {start: {artifact_id:"ART-IDR-BUNDLE-001"}, end: {icd_code:"C50.411"}, properties:{}}, {start: {artifact_id:"ART-IDR-BUNDLE-001"}, end: {icd_code:"E11.9"}, properties:{}}, {start: {artifact_id:"ART-IDR-BUNDLE-001"}, end: {icd_code:"Z90.13"}, properties:{}}] AS row
MATCH (start:Artifact{artifact_id: row.start.artifact_id})
MATCH (end:ICDCode{icd_code: row.end.icd_code})
CREATE (start)-[r:INCLUDES]->(end) SET r += row.properties;
UNWIND [{start: {procedure_id:"PROC-001"}, end: {case_id:"CASE-2026-001"}, properties:{}}] AS row
MATCH (start:Procedure{procedure_id: row.start.procedure_id})
MATCH (end:Case{case_id: row.end.case_id})
CREATE (start)-[r:PART_OF]->(end) SET r += row.properties;
UNWIND [{start: {procedure_id:"PROC-RECON-001"}, end: {diagnosis_id:"DX-001"}, properties:{}}] AS row
MATCH (start:Procedure{procedure_id: row.start.procedure_id})
MATCH (end:Diagnosis{diagnosis_id: row.end.diagnosis_id})
CREATE (start)-[r:JUSTIFIED_BY]->(end) SET r += row.properties;
UNWIND [{start: {graph_snapshot_id:"SNAP-2026-03-18-001"}, end: {artifact_id:"ART-OPNOTE-001"}, properties:{}}] AS row
MATCH (start:GraphSnapshotNode{graph_snapshot_id: row.start.graph_snapshot_id})
MATCH (end:Artifact{artifact_id: row.end.artifact_id})
CREATE (start)-[r:CAPTURES]->(end) SET r += row.properties;
UNWIND [{start: {finding_id:"FIND-INTRA-RECON-001"}, end: {procedure_id:"PROC-RECON-001"}, properties:{}}] AS row
MATCH (start:Finding{finding_id: row.start.finding_id})
MATCH (end:Procedure{procedure_id: row.end.procedure_id})
CREATE (start)-[r:SUPPORTED_BY]->(end) SET r += row.properties;
UNWIND [{start: {_id:39}, end: {_id:40}, properties:{}}] AS row
MATCH (start:`UNIQUE IMPORT LABEL`{`UNIQUE IMPORT ID`: row.start._id})
MATCH (end:`UNIQUE IMPORT LABEL`{`UNIQUE IMPORT ID`: row.end._id})
CREATE (start)-[r:CONTAINS]->(end) SET r += row.properties;
UNWIND [{start: {artifact_id:"ART-OPNOTE-001"}, end: {cpt_code:"19301"}, properties:{}}, {start: {artifact_id:"ART-OPNOTE-001"}, end: {cpt_code:"38525"}, properties:{}}, {start: {artifact_id:"ART-OPNOTE-001"}, end: {cpt_code:"38900"}, properties:{}}, {start: {artifact_id:"ART-OPNOTE-001"}, end: {cpt_code:"19364"}, properties:{}}, {start: {artifact_id:"ART-IDR-BUNDLE-001"}, end: {cpt_code:"19301"}, properties:{}}, {start: {artifact_id:"ART-IDR-BUNDLE-001"}, end: {cpt_code:"38525"}, properties:{}}, {start: {artifact_id:"ART-IDR-BUNDLE-001"}, end: {cpt_code:"38900"}, properties:{}}, {start: {artifact_id:"ART-IDR-BUNDLE-001"}, end: {cpt_code:"19364"}, properties:{}}] AS row
MATCH (start:Artifact{artifact_id: row.start.artifact_id})
MATCH (end:CPTCode{cpt_code: row.end.cpt_code})
CREATE (start)-[r:INCLUDES]->(end) SET r += row.properties;
UNWIND [{start: {graph_snapshot_id:"SNAP-2026-03-18-001"}, end: {case_id:"CASE-2026-001"}, properties:{}}] AS row
MATCH (start:GraphSnapshotNode{graph_snapshot_id: row.start.graph_snapshot_id})
MATCH (end:Case{case_id: row.end.case_id})
CREATE (start)-[r:CAPTURES]->(end) SET r += row.properties;
UNWIND [{start: {artifact_id:"ART-IDR-BUNDLE-001"}, end: {arbitration_id:"ARB-001-2026"}, properties:{}}] AS row
MATCH (start:Artifact{artifact_id: row.start.artifact_id})
MATCH (end:Arbitration{arbitration_id: row.end.arbitration_id})
CREATE (start)-[r:SUPPORTED_BY]->(end) SET r += row.properties;
UNWIND [{start: {event_id:"PROV-STATUS-UPDATE-001"}, end: {finding_id:"FIND-POSTOP-PATH-001"}, properties:{}}] AS row
MATCH (start:Provenance{event_id: row.start.event_id})
MATCH (end:Finding{finding_id: row.end.finding_id})
CREATE (start)-[r:RECORDED_FOR]->(end) SET r += row.properties;
UNWIND [{start: {_id:45}, end: {learning_node_id:"LEARN-CASE-2026-001"}, properties:{}}] AS row
MATCH (start:`UNIQUE IMPORT LABEL`{`UNIQUE IMPORT ID`: row.start._id})
MATCH (end:LearningNode_CASE{learning_node_id: row.end.learning_node_id})
CREATE (start)-[r:FEEDS_LEARNING]->(end) SET r += row.properties;
UNWIND [{start: {finding_id:"FIND-PREOP-001"}, end: {diagnosis_id:"DX-001"}, properties:{}}, {start: {finding_id:"FIND-POSTOP-001"}, end: {diagnosis_id:"DX-001"}, properties:{}}, {start: {finding_id:"FIND-POSTOP-PATH-001"}, end: {diagnosis_id:"DX-001"}, properties:{}}, {start: {finding_id:"FIND-INTRA-001"}, end: {diagnosis_id:"DX-001"}, properties:{}}] AS row
MATCH (start:Finding{finding_id: row.start.finding_id})
MATCH (end:Diagnosis{diagnosis_id: row.end.diagnosis_id})
CREATE (start)-[r:SUPPORTED_BY]->(end) SET r += row.properties;
UNWIND [{start: {procedure_id:"PROC-001"}, end: {action_id:"ACT-SLNB-001"}, properties:{}}, {start: {procedure_id:"PROC-001"}, end: {action_id:"ACT-EXC-001"}, properties:{}}, {start: {procedure_id:"PROC-RECON-001"}, end: {action_id:"ACT-DIEP-001"}, properties:{}}] AS row
MATCH (start:Procedure{procedure_id: row.start.procedure_id})
MATCH (end:Action{action_id: row.end.action_id})
CREATE (start)-[r:COMPOSED_OF]->(end) SET r += row.properties;
UNWIND [{start: {arbitration_id:"ARB-001-2026"}, end: {cpt_code:"19301"}, properties:{}}] AS row
MATCH (start:Arbitration{arbitration_id: row.start.arbitration_id})
MATCH (end:CPTCode{cpt_code: row.end.cpt_code})
CREATE (start)-[r:REFERENCES]->(end) SET r += row.properties;
UNWIND [{start: {diagnosis_id:"DX-001"}, end: {finding_id:"FIND-PREOP-001"}, properties:{}}, {start: {diagnosis_id:"DX-001"}, end: {finding_id:"FIND-POSTOP-001"}, properties:{}}, {start: {diagnosis_id:"DX-001"}, end: {finding_id:"FIND-POSTOP-PATH-001"}, properties:{}}, {start: {diagnosis_id:"DX-001"}, end: {finding_id:"FIND-INTRA-001"}, properties:{}}] AS row
MATCH (start:Diagnosis{diagnosis_id: row.start.diagnosis_id})
MATCH (end:Finding{finding_id: row.end.finding_id})
CREATE (start)-[r:SUPPORTED_BY]->(end) SET r += row.properties;
UNWIND [{start: {procedure_id:"PROC-RECON-001"}, end: {finding_id:"FIND-INTRA-RECON-001"}, properties:{}}] AS row
MATCH (start:Procedure{procedure_id: row.start.procedure_id})
MATCH (end:Finding{finding_id: row.end.finding_id})
CREATE (start)-[r:SUPPORTED_BY]->(end) SET r += row.properties;
UNWIND [{start: {event_id:"PROV-RECON-DOC-001"}, end: {procedure_id:"PROC-RECON-001"}, properties:{}}] AS row
MATCH (start:Provenance{event_id: row.start.event_id})
MATCH (end:Procedure{procedure_id: row.end.procedure_id})
CREATE (start)-[r:RECORDED_FOR]->(end) SET r += row.properties;
UNWIND [{start: {procedure_id:"PROC-001"}, end: {intent_id:"INTENT-BCT-001"}, properties:{}}] AS row
MATCH (start:Procedure{procedure_id: row.start.procedure_id})
MATCH (end:ClinicalIntent{intent_id: row.end.intent_id})
CREATE (start)-[r:ANTICIPATED_BY]->(end) SET r += row.properties;
MATCH (n:`UNIQUE IMPORT LABEL`)  WITH n LIMIT 200 REMOVE n:`UNIQUE IMPORT LABEL` REMOVE n.`UNIQUE IMPORT ID`;
DROP CONSTRAINT UNIQUE_IMPORT_NAME;
"
