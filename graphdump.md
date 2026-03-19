"CREATE CONSTRAINT UNIQUE_IMPORT_NAME FOR (node:`UNIQUE IMPORT LABEL`) REQUIRE (node.`UNIQUE IMPORT ID`) IS UNIQUE;
UNWIND [{_id:10, properties:{cpt_label:"Mastectomy, partial (e.g., lumpectomy, tylectomy, quadrantectomy, segmentectomy)", domain:"breast", cpt_code:"19301", unit_count:1}}, {_id:17, properties:{cpt_label:"Biopsy or excision of lymph node(s); open, deep axillary node(s)", domain:"lymph_node", cpt_code:"38525", unit_count:1}}, {_id:18, properties:{cpt_label:"Intraoperative identification (e.g., mapping) of sentinel lymph node(s)", domain:"intraoperative_mapping", cpt_code:"38900", unit_count:1}}, {_id:27, properties:{cpt_label:"Breast reconstruction with free flap (microvascular)", domain:"reconstruction", cpt_code:"19364", unit_count:1}}] AS row
CREATE (n:`UNIQUE IMPORT LABEL`{`UNIQUE IMPORT ID`: row._id}) SET n += row.properties SET n:CPTCode;
UNWIND [{_id:4, properties:{finding_id:"FIND-PREOP-001", clinical_phase:"preoperative", finding_label:"2 cm palpable mass in upper outer quadrant", source_document:"clinic_note_2026-03-10.pdf", finding_type:"preoperative", finding_class:"clinical_exam", timestamp:"2026-03-10T14:30:00Z"}}, {_id:13, properties:{finding_id:"FIND-POSTOP-001", clinical_phase:"postoperative", finding_label:"Pathology confirms clear margins, no residual tumor", source_document:"pathology_report_2026-04-20.pdf", finding_type:"postoperative", finding_class:"pathology_report", timestamp:"2026-04-20T11:00:00Z"}}, {_id:14, properties:{finding_id:"FIND-POSTOP-PATH-001", clinical_phase:"postoperative", finding_label:"Pathology: invasive ductal carcinoma, clear margins (2 mm), no LVI", source_document:"path_report_2026-04-20.pdf", finding_type:"postoperative", finding_class:"pathology", timestamp:"2026-04-20T14:15:00Z"}}, {_id:21, properties:{finding_id:"FIND-INTRA-001", clinical_phase:"intraoperative", finding_label:"Intraoperative frozen section: negative for residual tumor at margins", source_document:"intraop_frozen_section_2026-04-15.pdf", finding_type:"intraoperative", finding_class:"frozen_section_pathology", timestamp:"2026-04-15T10:15:00Z"}}, {_id:32, properties:{finding_id:"FIND-INTRA-RECON-001", clinical_phase:"intraoperative", finding_label:"Intraoperative indocyanine green angiography confirms excellent flap perfusion and no venous congestion", source_document:"intraop_icg_angiography_2026-07-15.pdf", finding_type:"intraoperative", finding_class:"angiography_assessment", timestamp:"2026-07-15T10:30:00Z"}}] AS row
CREATE (n:`UNIQUE IMPORT LABEL`{`UNIQUE IMPORT ID`: row._id}) SET n += row.properties SET n:Finding;
UNWIND [{_id:6, properties:{icd_code:"C50.411", diagnosis_id:"DX-001", diagnosis_label:"Invasive ductal carcinoma of right breast", diagnosis_status:"postoperative_confirmed"}}] AS row
CREATE (n:`UNIQUE IMPORT LABEL`{`UNIQUE IMPORT ID`: row._id}) SET n += row.properties SET n:Diagnosis;
UNWIND [{_id:8, properties:{procedure_label:"Partial mastectomy with sentinel lymph node biopsy", procedure_role:"primary", procedure_id:"PROC-001", procedure_species:"management_driven", execution_context:"elective", timestamp:"2026-04-15"}}, {_id:24, properties:{procedure_label:"Delayed autologous breast reconstruction (DIEP flap)", procedure_role:"secondary", procedure_id:"PROC-RECON-001", procedure_species:"management_driven", execution_context:"elective", timestamp:"2026-06-01"}}, {_id:28, properties:{procedure_label:"Delayed deep inferior epigastric perforator (DIEP) flap breast reconstruction", procedure_role:"secondary", procedure_id:"PROC-RECON-001", procedure_species:"management_driven", execution_context:"elective", timestamp:"2026-07-15"}}] AS row
CREATE (n:`UNIQUE IMPORT LABEL`{`UNIQUE IMPORT ID`: row._id}) SET n += row.properties SET n:Procedure;
UNWIND [{_id:7, properties:{intent_type:"therapeutic_strategy", intent_context:"Stage I-II disease, patient preference for conservation", intent_label:"Breast conserving therapy with sentinel node biopsy", created_timestamp:"2026-03-12T09:15:00Z", intent_id:"INTENT-BCT-001"}}] AS row
CREATE (n:`UNIQUE IMPORT LABEL`{`UNIQUE IMPORT ID`: row._id}) SET n += row.properties SET n:ClinicalIntent;
UNWIND [{_id:16, properties:{submission_date:"2026-05-10", cooling_off_period:"30 days", resolution_date:"2026-08-01", case_status:"resolved", arbitration_id:"ARB-001-2026", resolution_notes:"Payer agreed to full reimbursement after review of operative report, codes, and flap viability finding", payer:"UnitedHealthcare"}}] AS row
CREATE (n:`UNIQUE IMPORT LABEL`{`UNIQUE IMPORT ID`: row._id}) SET n += row.properties SET n:Arbitration;
UNWIND [{_id:1, properties:{action_class:"biopsy", action_id:"ACT-SLNB-001", execution_context:"intraoperative", procedural_domain:"staging", action_label:"Sentinel lymph node mapping and biopsy", timestamp:"2026-04-15T09:20:00Z", anatomic_target:"axillary lymph nodes"}}, {_id:9, properties:{action_class:"excision", action_id:"ACT-EXC-001", execution_context:"intraoperative", procedural_domain:"oncologic_excision", action_label:"Wide local excision of primary tumor", timestamp:"2026-04-15T08:45:00Z", anatomic_target:"breast mass"}}, {_id:25, properties:{action_class:"flap_reconstruction", action_id:"ACT-DIEP-001", execution_context:"intraoperative", procedural_domain:"reconstructive_transfer", action_label:"Deep inferior epigastric perforator flap harvest and microvascular transfer", timestamp:"2026-06-01T07:30:00Z", anatomic_target:"abdomen to right breast"}}, {_id:29, properties:{action_class:"microvascular_flap", action_id:"ACT-DIEP-001", execution_context:"intraoperative", procedural_domain:"reconstructive_transfer", action_label:"DIEP flap harvest from abdomen with microvascular anastomosis to internal mammary vessels", timestamp:"2026-07-15T08:00:00Z", anatomic_target:"abdomen to right breast"}}] AS row
CREATE (n:`UNIQUE IMPORT LABEL`{`UNIQUE IMPORT ID`: row._id}) SET n += row.properties SET n:Action;
UNWIND [{_id:12, properties:{actor:"SEF-System-v1.0", event_id:"PROV-ART-GEN-001", event_type:"artifact_generation", system_state:"draft_mode", timestamp:"2026-04-16T10:30:00Z"}}, {_id:15, properties:{actor:"SURG-456", event_id:"PROV-STATUS-UPDATE-001", event_type:"diagnosis_status_update", notes:"Reviewed pathology report; confirmed clear margins and updated status", system_state:"postop_review_complete", timestamp:"2026-04-21T08:45:00Z"}}, {_id:23, properties:{actor:"BILLING-SPEC-789", event_id:"PROV-IDR-PREP-001", event_type:"artifact_preparation", notes:"Compiled operative report, codes, and arbitration details for UHC dispute", system_state:"pre-submission_review", timestamp:"2026-05-15T09:00:00Z"}}, {_id:31, properties:{actor:"SURG-456", event_id:"PROV-RECON-DOC-001", event_type:"procedure_documentation", notes:"Dictated operative note for DIEP flap reconstruction; confirmed microvascular patency", system_state:"postop_documentation", timestamp:"2026-07-16T11:00:00Z"}}, {_id:33, properties:{actor:"SEF-Billing-Team", event_id:"PROV-ARB-RES-001", event_type:"arbitration_resolution", notes:"UHC reversed initial denial; all CPTs paid based on comprehensive evidence chain", system_state:"resolved_full_payment", timestamp:"2026-08-01T14:00:00Z"}}] AS row
CREATE (n:`UNIQUE IMPORT LABEL`{`UNIQUE IMPORT ID`: row._id}) SET n += row.properties SET n:Provenance;
UNWIND [{_id:3, properties:{patient_id:"PT-987654", case_id:"CASE-2026-001", surgeon_id:"SURG-456", facility_id:"HOSP-OC-01", procedure_date:"2026-04-15", specialty_modules_loaded:["Breast", "Oncologic"], case_context:"Breast oncology referral"}}] AS row
CREATE (n:`UNIQUE IMPORT LABEL`{`UNIQUE IMPORT ID`: row._id}) SET n += row.properties SET n:Case;
UNWIND [{_id:0, properties:{icd_code:"C50.411", coding_version:"ICD-10-CM 2026", icd_label:"Malignant neoplasm of upper-outer quadrant of right female breast"}}, {_id:19, properties:{icd_code:"E11.9", coding_version:"ICD-10-CM 2026", icd_label:"Type 2 diabetes mellitus without complications"}}, {_id:20, properties:{icd_code:"Z90.13", coding_version:"ICD-10-CM 2026", icd_label:"Acquired absence of bilateral breasts and nipples"}}] AS row
CREATE (n:`UNIQUE IMPORT LABEL`{`UNIQUE IMPORT ID`: row._id}) SET n += row.properties SET n:ICDCode;
UNWIND [{_id:2, properties:{ontology_reference:"SNOMED:48543004", region:"axilla", anatomy_id:"ANAT-AXILLA-R", laterality:"right", anatomic_label:"Right axillary lymph nodes"}}, {_id:5, properties:{ontology_reference:"SNOMED:76752008", region:"upper_outer_quadrant", anatomy_id:"ANAT-BREAST-R-UOQ", laterality:"right", anatomic_label:"Right breast upper outer quadrant"}}, {_id:26, properties:{ontology_reference:"SNOMED:69830009", region:"abdomen", anatomy_id:"ANAT-ABDOMEN", laterality:"bilateral", anatomic_label:"Lower abdomen (DIEP donor site)"}}, {_id:30, properties:{ontology_reference:"SNOMED:69830009", region:"abdomen", anatomy_id:"ANAT-ABDOMEN-LOWER", laterality:"bilateral", anatomic_label:"Lower abdominal wall (DIEP donor site)"}}] AS row
CREATE (n:`UNIQUE IMPORT LABEL`{`UNIQUE IMPORT ID`: row._id}) SET n += row.properties SET n:Anatomical;
UNWIND [{_id:11, properties:{artifact_type:"operative_report", generation_timestamp:"2026-04-16T10:30:00Z", artifact_id:"ART-OPNOTE-001", artifact_status:"draft"}}, {_id:22, properties:{artifact_type:"idr_submission_bundle", generation_timestamp:"2026-05-15T09:00:00Z", artifact_id:"ART-IDR-BUNDLE-001", artifact_status:"prepared"}}] AS row
CREATE (n:`UNIQUE IMPORT LABEL`{`UNIQUE IMPORT ID`: row._id}) SET n += row.properties SET n:Artifact;
UNWIND [{start: {_id:21}, end: {_id:9}, properties:{}}, {start: {_id:32}, end: {_id:25}, properties:{}}, {start: {_id:32}, end: {_id:29}, properties:{}}] AS row
MATCH (start:`UNIQUE IMPORT LABEL`{`UNIQUE IMPORT ID`: row.start._id})
MATCH (end:`UNIQUE IMPORT LABEL`{`UNIQUE IMPORT ID`: row.end._id})
CREATE (start)-[r:SUPPORTED_BY]->(end) SET r += row.properties;
UNWIND [{start: {_id:8}, end: {_id:3}, properties:{}}] AS row
MATCH (start:`UNIQUE IMPORT LABEL`{`UNIQUE IMPORT ID`: row.start._id})
MATCH (end:`UNIQUE IMPORT LABEL`{`UNIQUE IMPORT ID`: row.end._id})
CREATE (start)-[r:PART_OF]->(end) SET r += row.properties;
UNWIND [{start: {_id:16}, end: {_id:10}, properties:{}}] AS row
MATCH (start:`UNIQUE IMPORT LABEL`{`UNIQUE IMPORT ID`: row.start._id})
MATCH (end:`UNIQUE IMPORT LABEL`{`UNIQUE IMPORT ID`: row.end._id})
CREATE (start)-[r:REFERENCES]->(end) SET r += row.properties;
UNWIND [{start: {_id:24}, end: {_id:6}, properties:{}}, {start: {_id:28}, end: {_id:6}, properties:{}}] AS row
MATCH (start:`UNIQUE IMPORT LABEL`{`UNIQUE IMPORT ID`: row.start._id})
MATCH (end:`UNIQUE IMPORT LABEL`{`UNIQUE IMPORT ID`: row.end._id})
CREATE (start)-[r:JUSTIFIED_BY]->(end) SET r += row.properties;
UNWIND [{start: {_id:6}, end: {_id:0}, properties:{}}, {start: {_id:6}, end: {_id:19}, properties:{}}, {start: {_id:6}, end: {_id:20}, properties:{}}] AS row
MATCH (start:`UNIQUE IMPORT LABEL`{`UNIQUE IMPORT ID`: row.start._id})
MATCH (end:`UNIQUE IMPORT LABEL`{`UNIQUE IMPORT ID`: row.end._id})
CREATE (start)-[r:MAPS_TO]->(end) SET r += row.properties;
UNWIND [{start: {_id:31}, end: {_id:25}, properties:{}}, {start: {_id:31}, end: {_id:29}, properties:{}}] AS row
MATCH (start:`UNIQUE IMPORT LABEL`{`UNIQUE IMPORT ID`: row.start._id})
MATCH (end:`UNIQUE IMPORT LABEL`{`UNIQUE IMPORT ID`: row.end._id})
CREATE (start)-[r:RECORDED_FOR]->(end) SET r += row.properties;
UNWIND [{start: {_id:4}, end: {_id:5}, properties:{}}, {start: {_id:13}, end: {_id:5}, properties:{}}, {start: {_id:14}, end: {_id:5}, properties:{}}, {start: {_id:21}, end: {_id:5}, properties:{}}, {start: {_id:32}, end: {_id:30}, properties:{}}] AS row
MATCH (start:`UNIQUE IMPORT LABEL`{`UNIQUE IMPORT ID`: row.start._id})
MATCH (end:`UNIQUE IMPORT LABEL`{`UNIQUE IMPORT ID`: row.end._id})
CREATE (start)-[r:LOCATED_IN]->(end) SET r += row.properties;
UNWIND [{start: {_id:8}, end: {_id:7}, properties:{}}, {start: {_id:24}, end: {_id:7}, properties:{}}] AS row
MATCH (start:`UNIQUE IMPORT LABEL`{`UNIQUE IMPORT ID`: row.start._id})
MATCH (end:`UNIQUE IMPORT LABEL`{`UNIQUE IMPORT ID`: row.end._id})
CREATE (start)-[r:ANTICIPATED_BY]->(end) SET r += row.properties;
UNWIND [{start: {_id:11}, end: {_id:10}, properties:{}}, {start: {_id:11}, end: {_id:17}, properties:{}}, {start: {_id:11}, end: {_id:18}, properties:{}}, {start: {_id:11}, end: {_id:27}, properties:{}}, {start: {_id:22}, end: {_id:10}, properties:{}}, {start: {_id:22}, end: {_id:17}, properties:{}}, {start: {_id:22}, end: {_id:18}, properties:{}}, {start: {_id:22}, end: {_id:27}, properties:{}}] AS row
MATCH (start:`UNIQUE IMPORT LABEL`{`UNIQUE IMPORT ID`: row.start._id})
MATCH (end:`UNIQUE IMPORT LABEL`{`UNIQUE IMPORT ID`: row.end._id})
CREATE (start)-[r:INCLUDES]->(end) SET r += row.properties;
UNWIND [{start: {_id:16}, end: {_id:11}, properties:{}}] AS row
MATCH (start:`UNIQUE IMPORT LABEL`{`UNIQUE IMPORT ID`: row.start._id})
MATCH (end:`UNIQUE IMPORT LABEL`{`UNIQUE IMPORT ID`: row.end._id})
CREATE (start)-[r:SUBMITTED_WITH]->(end) SET r += row.properties;
UNWIND [{start: {_id:7}, end: {_id:8}, properties:{}}] AS row
MATCH (start:`UNIQUE IMPORT LABEL`{`UNIQUE IMPORT ID`: row.start._id})
MATCH (end:`UNIQUE IMPORT LABEL`{`UNIQUE IMPORT ID`: row.end._id})
CREATE (start)-[r:ANTICIPATES]->(end) SET r += row.properties;
UNWIND [{start: {_id:12}, end: {_id:3}, properties:{}}, {start: {_id:15}, end: {_id:3}, properties:{}}, {start: {_id:23}, end: {_id:3}, properties:{}}, {start: {_id:31}, end: {_id:3}, properties:{}}, {start: {_id:33}, end: {_id:3}, properties:{}}] AS row
MATCH (start:`UNIQUE IMPORT LABEL`{`UNIQUE IMPORT ID`: row.start._id})
MATCH (end:`UNIQUE IMPORT LABEL`{`UNIQUE IMPORT ID`: row.end._id})
CREATE (start)-[r:RECORDED_FOR]->(end) SET r += row.properties;
UNWIND [{start: {_id:4}, end: {_id:6}, properties:{}}, {start: {_id:13}, end: {_id:6}, properties:{}}, {start: {_id:14}, end: {_id:6}, properties:{}}, {start: {_id:21}, end: {_id:6}, properties:{}}] AS row
MATCH (start:`UNIQUE IMPORT LABEL`{`UNIQUE IMPORT ID`: row.start._id})
MATCH (end:`UNIQUE IMPORT LABEL`{`UNIQUE IMPORT ID`: row.end._id})
CREATE (start)-[r:SUPPORTED_BY]->(end) SET r += row.properties;
UNWIND [{start: {_id:22}, end: {_id:11}, properties:{}}] AS row
MATCH (start:`UNIQUE IMPORT LABEL`{`UNIQUE IMPORT ID`: row.start._id})
MATCH (end:`UNIQUE IMPORT LABEL`{`UNIQUE IMPORT ID`: row.end._id})
CREATE (start)-[r:SUPPORTED_BY]->(end) SET r += row.properties;
UNWIND [{start: {_id:8}, end: {_id:1}, properties:{}}, {start: {_id:8}, end: {_id:9}, properties:{}}, {start: {_id:24}, end: {_id:25}, properties:{}}, {start: {_id:28}, end: {_id:29}, properties:{}}] AS row
MATCH (start:`UNIQUE IMPORT LABEL`{`UNIQUE IMPORT ID`: row.start._id})
MATCH (end:`UNIQUE IMPORT LABEL`{`UNIQUE IMPORT ID`: row.end._id})
CREATE (start)-[r:COMPOSED_OF]->(end) SET r += row.properties;
UNWIND [{start: {_id:3}, end: {_id:4}, properties:{}}, {start: {_id:3}, end: {_id:13}, properties:{}}, {start: {_id:3}, end: {_id:14}, properties:{}}, {start: {_id:3}, end: {_id:21}, properties:{}}, {start: {_id:3}, end: {_id:32}, properties:{}}] AS row
MATCH (start:`UNIQUE IMPORT LABEL`{`UNIQUE IMPORT ID`: row.start._id})
MATCH (end:`UNIQUE IMPORT LABEL`{`UNIQUE IMPORT ID`: row.end._id})
CREATE (start)-[r:HAS_FINDING]->(end) SET r += row.properties;
UNWIND [{start: {_id:8}, end: {_id:10}, properties:{}}, {start: {_id:8}, end: {_id:17}, properties:{}}, {start: {_id:8}, end: {_id:18}, properties:{}}, {start: {_id:24}, end: {_id:27}, properties:{}}, {start: {_id:28}, end: {_id:27}, properties:{}}] AS row
MATCH (start:`UNIQUE IMPORT LABEL`{`UNIQUE IMPORT ID`: row.start._id})
MATCH (end:`UNIQUE IMPORT LABEL`{`UNIQUE IMPORT ID`: row.end._id})
CREATE (start)-[r:MAPS_TO]->(end) SET r += row.properties;
UNWIND [{start: {_id:3}, end: {_id:24}, properties:{}}, {start: {_id:3}, end: {_id:28}, properties:{}}] AS row
MATCH (start:`UNIQUE IMPORT LABEL`{`UNIQUE IMPORT ID`: row.start._id})
MATCH (end:`UNIQUE IMPORT LABEL`{`UNIQUE IMPORT ID`: row.end._id})
CREATE (start)-[r:HAS_PROCEDURE]->(end) SET r += row.properties;
UNWIND [{start: {_id:32}, end: {_id:24}, properties:{}}, {start: {_id:32}, end: {_id:28}, properties:{}}] AS row
MATCH (start:`UNIQUE IMPORT LABEL`{`UNIQUE IMPORT ID`: row.start._id})
MATCH (end:`UNIQUE IMPORT LABEL`{`UNIQUE IMPORT ID`: row.end._id})
CREATE (start)-[r:SUPPORTED_BY]->(end) SET r += row.properties;
UNWIND [{start: {_id:3}, end: {_id:11}, properties:{}}, {start: {_id:3}, end: {_id:22}, properties:{}}] AS row
MATCH (start:`UNIQUE IMPORT LABEL`{`UNIQUE IMPORT ID`: row.start._id})
MATCH (end:`UNIQUE IMPORT LABEL`{`UNIQUE IMPORT ID`: row.end._id})
CREATE (start)-[r:GENERATES]->(end) SET r += row.properties;
UNWIND [{start: {_id:23}, end: {_id:16}, properties:{}}, {start: {_id:33}, end: {_id:16}, properties:{}}] AS row
MATCH (start:`UNIQUE IMPORT LABEL`{`UNIQUE IMPORT ID`: row.start._id})
MATCH (end:`UNIQUE IMPORT LABEL`{`UNIQUE IMPORT ID`: row.end._id})
CREATE (start)-[r:RECORDED_FOR]->(end) SET r += row.properties;
UNWIND [{start: {_id:1}, end: {_id:2}, properties:{}}, {start: {_id:9}, end: {_id:5}, properties:{}}, {start: {_id:25}, end: {_id:26}, properties:{}}, {start: {_id:29}, end: {_id:30}, properties:{}}] AS row
MATCH (start:`UNIQUE IMPORT LABEL`{`UNIQUE IMPORT ID`: row.start._id})
MATCH (end:`UNIQUE IMPORT LABEL`{`UNIQUE IMPORT ID`: row.end._id})
CREATE (start)-[r:PERFORMED_ON]->(end) SET r += row.properties;
UNWIND [{start: {_id:6}, end: {_id:4}, properties:{}}, {start: {_id:6}, end: {_id:13}, properties:{}}, {start: {_id:6}, end: {_id:14}, properties:{}}, {start: {_id:6}, end: {_id:21}, properties:{}}] AS row
MATCH (start:`UNIQUE IMPORT LABEL`{`UNIQUE IMPORT ID`: row.start._id})
MATCH (end:`UNIQUE IMPORT LABEL`{`UNIQUE IMPORT ID`: row.end._id})
CREATE (start)-[r:SUPPORTED_BY]->(end) SET r += row.properties;
UNWIND [{start: {_id:6}, end: {_id:7}, properties:{}}] AS row
MATCH (start:`UNIQUE IMPORT LABEL`{`UNIQUE IMPORT ID`: row.start._id})
MATCH (end:`UNIQUE IMPORT LABEL`{`UNIQUE IMPORT ID`: row.end._id})
CREATE (start)-[r:GENERATES_INTENT]->(end) SET r += row.properties;
UNWIND [{start: {_id:31}, end: {_id:24}, properties:{}}, {start: {_id:31}, end: {_id:28}, properties:{}}] AS row
MATCH (start:`UNIQUE IMPORT LABEL`{`UNIQUE IMPORT ID`: row.start._id})
MATCH (end:`UNIQUE IMPORT LABEL`{`UNIQUE IMPORT ID`: row.end._id})
CREATE (start)-[r:RECORDED_FOR]->(end) SET r += row.properties;
UNWIND [{start: {_id:11}, end: {_id:0}, properties:{}}, {start: {_id:11}, end: {_id:19}, properties:{}}, {start: {_id:11}, end: {_id:20}, properties:{}}, {start: {_id:22}, end: {_id:0}, properties:{}}, {start: {_id:22}, end: {_id:19}, properties:{}}, {start: {_id:22}, end: {_id:20}, properties:{}}] AS row
MATCH (start:`UNIQUE IMPORT LABEL`{`UNIQUE IMPORT ID`: row.start._id})
MATCH (end:`UNIQUE IMPORT LABEL`{`UNIQUE IMPORT ID`: row.end._id})
CREATE (start)-[r:INCLUDES]->(end) SET r += row.properties;
UNWIND [{start: {_id:15}, end: {_id:6}, properties:{}}] AS row
MATCH (start:`UNIQUE IMPORT LABEL`{`UNIQUE IMPORT ID`: row.start._id})
MATCH (end:`UNIQUE IMPORT LABEL`{`UNIQUE IMPORT ID`: row.end._id})
CREATE (start)-[r:RECORDED_FOR]->(end) SET r += row.properties;
UNWIND [{start: {_id:11}, end: {_id:8}, properties:{}}] AS row
MATCH (start:`UNIQUE IMPORT LABEL`{`UNIQUE IMPORT ID`: row.start._id})
MATCH (end:`UNIQUE IMPORT LABEL`{`UNIQUE IMPORT ID`: row.end._id})
CREATE (start)-[r:SUPPORTED_BY]->(end) SET r += row.properties;
UNWIND [{start: {_id:24}, end: {_id:32}, properties:{}}, {start: {_id:28}, end: {_id:32}, properties:{}}] AS row
MATCH (start:`UNIQUE IMPORT LABEL`{`UNIQUE IMPORT ID`: row.start._id})
MATCH (end:`UNIQUE IMPORT LABEL`{`UNIQUE IMPORT ID`: row.end._id})
CREATE (start)-[r:SUPPORTED_BY]->(end) SET r += row.properties;
UNWIND [{start: {_id:15}, end: {_id:14}, properties:{}}] AS row
MATCH (start:`UNIQUE IMPORT LABEL`{`UNIQUE IMPORT ID`: row.start._id})
MATCH (end:`UNIQUE IMPORT LABEL`{`UNIQUE IMPORT ID`: row.end._id})
CREATE (start)-[r:RECORDED_FOR]->(end) SET r += row.properties;
UNWIND [{start: {_id:16}, end: {_id:0}, properties:{}}] AS row
MATCH (start:`UNIQUE IMPORT LABEL`{`UNIQUE IMPORT ID`: row.start._id})
MATCH (end:`UNIQUE IMPORT LABEL`{`UNIQUE IMPORT ID`: row.end._id})
CREATE (start)-[r:REFERENCES]->(end) SET r += row.properties;
UNWIND [{start: {_id:22}, end: {_id:16}, properties:{}}] AS row
MATCH (start:`UNIQUE IMPORT LABEL`{`UNIQUE IMPORT ID`: row.start._id})
MATCH (end:`UNIQUE IMPORT LABEL`{`UNIQUE IMPORT ID`: row.end._id})
CREATE (start)-[r:SUPPORTED_BY]->(end) SET r += row.properties;
UNWIND [{start: {_id:25}, end: {_id:32}, properties:{}}, {start: {_id:29}, end: {_id:32}, properties:{}}] AS row
MATCH (start:`UNIQUE IMPORT LABEL`{`UNIQUE IMPORT ID`: row.start._id})
MATCH (end:`UNIQUE IMPORT LABEL`{`UNIQUE IMPORT ID`: row.end._id})
CREATE (start)-[r:SUPPORTED_BY]->(end) SET r += row.properties;
UNWIND [{start: {_id:12}, end: {_id:11}, properties:{}}, {start: {_id:23}, end: {_id:22}, properties:{}}, {start: {_id:33}, end: {_id:22}, properties:{}}] AS row
MATCH (start:`UNIQUE IMPORT LABEL`{`UNIQUE IMPORT ID`: row.start._id})
MATCH (end:`UNIQUE IMPORT LABEL`{`UNIQUE IMPORT ID`: row.end._id})
CREATE (start)-[r:RECORDED_FOR]->(end) SET r += row.properties;
MATCH (n:`UNIQUE IMPORT LABEL`)  WITH n LIMIT 200 REMOVE n:`UNIQUE IMPORT LABEL` REMOVE n.`UNIQUE IMPORT ID`;
DROP CONSTRAINT UNIQUE_IMPORT_NAME;
"
