import { VertexAI } from "@google-cloud/vertexai";

const vertexAI = new VertexAI({
  project: process.env.GCP_PROJECT_ID,
  location: process.env.GCP_LOCATION
});

export async function generateContent(prompt) {
  const model = vertexAI.getGenerativeModel({
    model: "gemini-1.0-pro"
  });

  const request = {
    contents: [
      {
        role: "user",
        parts: [{ text: prompt }]
      }
    ]
  };

  const response = await model.generateContent(request);
  return response.response.candidates[0].content.parts[0].text;
}