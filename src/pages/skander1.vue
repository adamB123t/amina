<template>
    <v-container class="fill-height d-flex flex-column justify-center align-center">
      <v-row class="mt-5">
        <v-col>
          <p class="text-center headline">{{ confirmationText }}</p>
        </v-col>
      </v-row>
      <v-row>
        <v-col>
          <v-btn @click="generatePDF" color="primary" large>Generate PDF Receipt</v-btn>
        </v-col>
      </v-row>
    </v-container>
  </template>
  
  <script>
  import jsPDF from 'jspdf';
  
  export default {
    data() {
      return {
        confirmationText: "Booking confirmed. Click below to receive your receipt."
      };
    },
    methods: {
      generatePDF() {
        const doc = new jsPDF();
        
        // Add title
        doc.setFontSize(22);
        const textWidth = doc.getStringUnitWidth('Booking Details:') * 16 / doc.internal.scaleFactor;
        const startX = (doc.internal.pageSize.width - textWidth) / 2;
        doc.setTextColor(255, 0, 0); 
        doc.text('Booking Details:', startX, 40); 
        
        doc.setFontSize(16);
        doc.setTextColor(0, 0, 0); // Reset text color to black
        
        doc.setTextColor(0, 128, 0);
        doc.text('Scooter ID:', 10, 60);
        doc.setTextColor(0, 0, 0);
        doc.text('XYZ123', 60, 60);
        
        // Scooter Location in green and location in black
        doc.setTextColor(0, 128, 0);
        doc.text('Scooter Location:', 10, 80);
        doc.setTextColor(0, 0, 0);
        doc.text('1053 Les Berges du Lac II Walkway, Tunis 1053', 60, 80);
        
        // Scooter Color in green and color in black
        doc.setTextColor(0, 128, 0);
        doc.text('Scooter Color:', 10, 100);
        doc.setTextColor(0, 0, 0);
        doc.text('Red', 60, 100);
        
        // Price of scooter
        doc.setTextColor(0, 128, 0);
        doc.text('Price of Scooter:', 10, 120);
        doc.setTextColor(0, 0, 0);
        doc.text('15 Dt per hour', 60, 120);
        
        // User Name in green and black
        doc.setTextColor(0, 128, 0);
        doc.text('Name:', 10, 160);
        doc.setTextColor(0, 0, 0);
        doc.text('Skander', 40, 160);
        
        // User Username in green and black
        doc.setTextColor(0, 128, 0);
        doc.text('Username:', 10, 180);
        doc.setTextColor(0, 0, 0);
        doc.text('Skander2904', 40, 180);
        
        // User Email in green and black 
        doc.setTextColor(0, 128, 0);
        doc.text('Email:', 10, 200);
        doc.setTextColor(0, 0, 0);
        doc.text('Skander@example.com', 40, 200);
        
        // User Number in green and black 
        doc.setTextColor(0, 128, 0);
        doc.text('Number:', 10, 220);
        doc.setTextColor(0, 0, 0);
        doc.text('+1234567890', 40, 220);
        
        // Save PDF
        doc.save('scooter_booking_receipt.pdf');
      }
    }
  }
  </script>
  
  <style scoped>
  .text-center {
    text-align: center;
  }
  
  .headline {
    font-size: 24px;
    font-weight: bold;
    color: #333;
    margin: 0; /* Remove default margin */
    padding: 10px; /* Add padding for better spacing */
  }
  </style>
  