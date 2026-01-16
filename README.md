<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Preoperative Clinic Assessment System</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        
        body {
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            padding: 20px;
        }
        
        .container {
            max-width: 1200px;
            margin: 0 auto;
            background: rgba(255, 255, 255, 0.95);
            border-radius: 20px;
            box-shadow: 0 20px 40px rgba(0, 0, 0, 0.1);
            overflow: hidden;
        }
        
        .header {
            background: linear-gradient(135deg, #2c3e50 0%, #34495e 100%);
            color: white;
            padding: 30px;
            text-align: center;
        }
        
        .header h1 {
            font-size: 2.5rem;
            font-weight: 700;
            margin-bottom: 10px;
        }
        
        .header p {
            font-size: 1.1rem;
            opacity: 0.9;
        }
        
        .content {
            padding: 30px;
        }
        
        .section {
            margin-bottom: 40px;
            background: white;
            border-radius: 15px;
            padding: 25px;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.08);
            border-left: 5px solid #3498db;
        }
        
        .section h2 {
            color: #2c3e50;
            font-size: 1.8rem;
            margin-bottom: 20px;
            display: flex;
            align-items: center;
            gap: 10px;
        }
        
        .form-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 20px;
        }
        
        .form-group {
            display: flex;
            flex-direction: column;
        }
        
        label {
            font-weight: 600;
            color: #34495e;
            margin-bottom: 8px;
            font-size: 0.95rem;
        }
        
        input, select, textarea {
            padding: 12px 15px;
            border: 2px solid #e1e8ed;
            border-radius: 10px;
            font-size: 1rem;
            transition: all 0.3s ease;
            background: #fafbfc;
        }
        
        input:focus, select:focus, textarea:focus {
            outline: none;
            border-color: #3498db;
            background: white;
            box-shadow: 0 0 0 3px rgba(52, 152, 219, 0.1);
        }
        
        textarea {
            resize: vertical;
            min-height: 100px;
        }
        
        .checkbox-group {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 15px;
            margin-top: 10px;
        }
        
        .checkbox-item {
            display: flex;
            align-items: center;
            gap: 10px;
            padding: 12px 15px;
            background: #f8f9fa;
            border-radius: 10px;
            border: 2px solid transparent;
            transition: all 0.3s ease;
            cursor: pointer;
        }
        
        .checkbox-item:hover {
            background: #e3f2fd;
            border-color: #3498db;
        }
        
        .checkbox-item input[type="checkbox"] {
            width: 18px;
            height: 18px;
            margin: 0;
        }
        
        .generate-btn {
            background: linear-gradient(135deg, #27ae60 0%, #2ecc71 100%);
            color: white;
            padding: 15px 30px;
            border: none;
            border-radius: 10px;
            font-size: 1.1rem;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s ease;
            box-shadow: 0 5px 15px rgba(46, 204, 113, 0.3);
            display: block;
            margin: 30px auto;
            min-width: 200px;
        }
        
        .generate-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 8px 25px rgba(46, 204, 113, 0.4);
        }
        
        .recommendations {
            margin-top: 30px;
            background: linear-gradient(135deg, #f8f9fa 0%, #e9ecef 100%);
            border-radius: 15px;
            padding: 25px;
            border: 2px solid #dee2e6;
            display: none;
        }
        
        .recommendations h3 {
            color: #2c3e50;
            font-size: 1.6rem;
            margin-bottom: 20px;
            text-align: center;
        }
        
        .rec-category {
            margin-bottom: 25px;
            background: white;
            border-radius: 10px;
            padding: 20px;
            box-shadow: 0 3px 10px rgba(0, 0, 0, 0.1);
        }
        
        .rec-category h4 {
            color: #e74c3c;
            font-size: 1.3rem;
            margin-bottom: 15px;
            padding-bottom: 8px;
            border-bottom: 2px solid #f1c40f;
        }
        
        .rec-list {
            list-style: none;
            padding: 0;
        }
        
        .rec-list li {
            padding: 8px 0;
            border-bottom: 1px solid #ecf0f1;
            color: #2c3e50;
            font-weight: 500;
        }
        
        .rec-list li:last-child {
            border-bottom: none;
        }
        
        .rec-list li::before {
            content: "✓ ";
            color: #27ae60;
            font-weight: bold;
            margin-right: 8px;
        }
        
        .icon {
            font-size: 1.2rem;
        }
        
        @media (max-width: 768px) {
            .form-grid {
                grid-template-columns: 1fr;
            }
            
            .checkbox-group {
                grid-template-columns: 1fr;
            }
            
            .header h1 {
                font-size: 2rem;
            }
            
            .content {
                padding: 20px;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="header">
            <h1>🏥 Preoperative Clinic Assessment</h1>
            <p>Comprehensive patient evaluation and order recommendations</p>
        </div>
        
        <div class="content">
            <form id="preopForm">
                <!-- Patient Information -->
                <div class="section">
                    <h2><span class="icon">👤</span> Patient Information</h2>
                    <div class="form-grid">
                        <div class="form-group">
                            <label for="patientName">Patient Name</label>
                            <input type="text" id="patientName" name="patientName" required>
                        </div>
                        <div class="form-group">
                            <label for="age">Age</label>
                            <input type="number" id="age" name="age" min="0" max="120" required>
                        </div>
                        <div class="form-group">
                            <label for="gender">Gender</label>
                            <select id="gender" name="gender" required>
                                <option value="">Select Gender</option>
                                <option value="male">Male</option>
                                <option value="female">Female</option>
                                <option value="other">Other</option>
                            </select>
                        </div>
                        <div class="form-group">
                            <label for="weight">Weight (kg)</label>
                            <input type="number" id="weight" name="weight" step="0.1">
                        </div>
                        <div class="form-group">
                            <label for="height">Height (cm)</label>
                            <input type="number" id="height" name="height">
                        </div>
                    </div>
                </div>

                <!-- Planned Surgery -->
                <div class="section">
                    <h2><span class="icon">🔧</span> Planned Surgery</h2>
                    <div class="form-grid">
                        <div class="form-group">
                            <label for="surgeryType">Type of Surgery</label>
                            <select id="surgeryType" name="surgeryType" required>
                                <option value="">Select Surgery Type</option>
                                <option value="cardiac">Cardiac Surgery</option>
                                <option value="orthopedic">Orthopedic Surgery</option>
                                <option value="abdominal">Abdominal Surgery</option>
                                <option value="neurological">Neurological Surgery</option>
                                <option value="thoracic">Thoracic Surgery</option>
                                <option value="urological">Urological Surgery</option>
                                <option value="gynecological">Gynecological Surgery</option>
                                <option value="ent">ENT Surgery</option>
                                <option value="plastic">Plastic Surgery</option>
                                <option value="vascular">Vascular Surgery</option>
                                <option value="other">Other</option>
                            </select>
                        </div>
                        <div class="form-group">
                            <label for="anesthesiaType">Planned Anesthesia</label>
                            <select id="anesthesiaType" name="anesthesiaType">
                                <option value="">Select Anesthesia Type</option>
                                <option value="general">General Anesthesia</option>
                                <option value="regional">Regional Anesthesia</option>
                                <option value="local">Local Anesthesia</option>
                                <option value="sedation">Sedation</option>
                            </select>
                        </div>
                        <div class="form-group">
                            <label for="surgeryDate">Scheduled Surgery Date</label>
                            <input type="date" id="surgeryDate" name="surgeryDate">
                        </div>
                    </div>
                </div>

                <!-- Medical History -->
                <div class="section">
                    <h2><span class="icon">📋</span> Medical History</h2>
                    <div class="checkbox-group">
                        <label class="checkbox-item">
                            <input type="checkbox" name="conditions" value="hypertension">
                            <span>Hypertension</span>
                        </label>
                        <label class="checkbox-item">
                            <input type="checkbox" name="conditions" value="diabetes">
                            <span>Diabetes Mellitus</span>
                        </label>
                        <label class="checkbox-item">
                            <input type="checkbox" name="conditions" value="heart_disease">
                            <span>Heart Disease</span>
                        </label>
                        <label class="checkbox-item">
                            <input type="checkbox" name="conditions" value="copd">
                            <span>COPD/Asthma</span>
                        </label>
                        <label class="checkbox-item">
                            <input type="checkbox" name="conditions" value="kidney_disease">
                            <span>Kidney Disease</span>
                        </label>
                        <label class="checkbox-item">
                            <input type="checkbox" name="conditions" value="liver_disease">
                            <span>Liver Disease</span>
                        </label>
                        <label class="checkbox-item">
                            <input type="checkbox" name="conditions" value="bleeding_disorder">
                            <span>Bleeding Disorder</span>
                        </label>
                        <label class="checkbox-item">
                            <input type="checkbox" name="conditions" value="stroke">
                            <span>Previous Stroke</span>
                        </label>
                        <label class="checkbox-item">
                            <input type="checkbox" name="conditions" value="cancer">
                            <span>Cancer History</span>
                        </label>
                        <label class="checkbox-item">
                            <input type="checkbox" name="conditions" value="anesthesia_complications">
                            <span>Previous Anesthesia Complications</span>
                        </label>
                    </div>
                    
                    <div class="form-grid" style="margin-top: 20px;">
                        <div class="form-group">
                            <label for="medications">Current Medications</label>
                            <textarea id="medications" name="medications" placeholder="List all current medications..."></textarea>
                        </div>
                        <div class="form-group">
                            <label for="allergies">Allergies</label>
                            <textarea id="allergies" name="allergies" placeholder="List all known allergies..."></textarea>
                        </div>
                    </div>
                </div>

                <!-- Functional Status -->
                <div class="section">
                    <h2><span class="icon">🏃</span> Functional Status</h2>
                    <div class="form-grid">
                        <div class="form-group">
                            <label for="functionalCapacity">Functional Capacity (METs)</label>
                            <select id="functionalCapacity" name="functionalCapacity">
                                <option value="">Select Functional Capacity</option>
                                <option value="poor">Poor (&lt;4 METs)</option>
                                <option value="moderate">Moderate (4-10 METs)</option>
                                <option value="excellent">Excellent (&gt;10 METs)</option>
                            </select>
                        </div>
                        <div class="form-group">
                            <label for="smokingStatus">Smoking Status</label>
                            <select id="smokingStatus" name="smokingStatus">
                                <option value="">Select Status</option>
                                <option value="never">Never Smoked</option>
                                <option value="former">Former Smoker</option>
                                <option value="current">Current Smoker</option>
                            </select>
                        </div>
                        <div class="form-group">
                            <label for="alcoholUse">Alcohol Use</label>
                            <select id="alcoholUse" name="alcoholUse">
                                <option value="">Select Usage</option>
                                <option value="none">None</option>
                                <option value="social">Social Drinking</option>
                                <option value="moderate">Moderate Use</option>
                                <option value="heavy">Heavy Use</option>
                            </select>
                        </div>
                    </div>
                </div>

                <button type="button" class="generate-btn" onclick="generateRecommendations()">Generate Preoperative Orders</button>
            </form>

            <div id="recommendations" class="recommendations">
                <h3>🎯 Recommended Preoperative Orders</h3>
                <div id="recommendationsContent"></div>
            </div>
        </div>
    </div>

    <script>
        function generateRecommendations() {
            // Get form data
            const age = parseInt(document.getElementById('age').value) || 0;
            const surgery = document.getElementById('surgeryType').value;
            const anesthesia = document.getElementById('anesthesiaType').value;
            
            // Get checked conditions
            const conditions = Array.from(document.querySelectorAll('input[name="conditions"]:checked'))
                .map(cb => cb.value);
            
            let html = '';
            
            // Laboratory Studies
            html += `
                <div class="rec-category">
                    <h4>🧪 Laboratory Studies</h4>
                    <ul class="rec-list">
                        <li>Complete Blood Count (CBC)</li>
                        <li>Basic Metabolic Panel (BMP)</li>
            `;
            
            if (age >= 50 || conditions.includes('diabetes') || conditions.includes('kidney_disease')) {
                html += `<li>Comprehensive Metabolic Panel (CMP)</li>`;
            }
            
            if (conditions.includes('bleeding_disorder') || surgery === 'cardiac' || surgery === 'neurological') {
                html += `<li>PT/PTT/INR</li>`;
            }
            
            if (surgery === 'cardiac' || surgery === 'orthopedic' || surgery === 'abdominal') {
                html += `<li>Type and Screen</li>`;
            }
            
            if (conditions.includes('diabetes')) {
                html += `<li>HbA1c</li>`;
            }
            
            if (conditions.includes('liver_disease')) {
                html += `<li>Liver Function Tests</li>`;
            }
            
            html += `</ul></div>`;
            
            // Diagnostic Studies
            html += `
                <div class="rec-category">
                    <h4>📊 Diagnostic Studies</h4>
                    <ul class="rec-list">
            `;
            
            if (age >= 40 || conditions.includes('heart_disease') || conditions.includes('hypertension')) {
                html += `<li>ECG (Electrocardiogram)</li>`;
            }
            
            if (conditions.includes('heart_disease') || surgery === 'cardiac') {
                html += `<li>Echocardiogram</li>`;
            }
            
            if (conditions.includes('copd')) {
                html += `<li>Pulmonary Function Tests</li>`;
            }
            
            html += `</ul></div>`;
            
            // Imaging Studies
            html += `
                <div class="rec-category">
                    <h4>📷 Imaging Studies</h4>
                    <ul class="rec-list">
            `;
            
            if (age >= 60 || conditions.includes('copd') || surgery === 'thoracic' || surgery === 'cardiac') {
                html += `<li>Chest X-ray</li>`;
            }
            
            if (surgery === 'orthopedic') {
                html += `<li>X-rays of surgical site</li>`;
            }
            
            html += `</ul></div>`;
            
            // Consultations
            if (conditions.length > 0) {
                html += `
                    <div class="rec-category">
                        <h4>👨‍⚕️ Specialist Consultations</h4>
                        <ul class="rec-list">
                `;
                
                if (conditions.includes('heart_disease')) {
                    html += `<li>Cardiology Consultation</li>`;
                }
                
                if (conditions.includes('copd')) {
                    html += `<li>Pulmonology Consultation</li>`;
                }
                
                if (conditions.includes('kidney_disease')) {
                    html += `<li>Nephrology Consultation</li>`;
                }
                
                if (conditions.includes('diabetes') && age >= 65) {
                    html += `<li>Endocrinology Consultation (if poorly controlled)</li>`;
                }
                
                html += `</ul></div>`;
            }
            
            // Medications
            html += `
                <div class="rec-category">
                    <h4>💊 Medication Management</h4>
                    <ul class="rec-list">
                        <li>Review all current medications</li>
                        <li>Consider holding anticoagulants per protocol</li>
                        <li>Continue beta-blockers and statins if prescribed</li>
            `;
            
            if (conditions.includes('diabetes')) {
                html += `<li>Adjust diabetes medications per anesthesia protocol</li>`;
            }
            
            html += `</ul></div>`;
            
            // Set the content and show recommendations
            document.getElementById('recommendationsContent').innerHTML = html;
            document.getElementById('recommendations').style.display = 'block';
            document.getElementById('recommendations').scrollIntoView({ behavior: 'smooth' });
        }
    </script>
</body>
</html>
