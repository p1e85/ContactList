package com.example.contactlist;

import java.io.FileInputStream;
import java.io.FileNotFoundException;
import java.io.FileOutputStream;
import java.io.IOException;

import org.json.JSONArray;
import org.json.JSONException;
import org.json.JSONObject;

import android.app.Activity;
import android.content.Context;
import android.os.Bundle;
import android.util.Log;
import android.view.Menu;
import android.view.MenuItem;
import android.view.View;
import android.widget.Button;
import android.widget.EditText;
import android.widget.Toast;

public class MainActivity extends Activity {

	JSONObject json, json1;
	JSONArray jsonArray;
	String serializedJson = null;

	EditText name, address, phone, email;
	Button save, load, clear;

	@Override
	protected void onCreate(Bundle savedInstanceState) {
		super.onCreate(savedInstanceState);
		setContentView(R.layout.activity_main);

		json = new JSONObject();
		json1 = new JSONObject();
		jsonArray = new JSONArray();

		name = (EditText) findViewById(R.id.etName);
		address = (EditText) findViewById(R.id.etAddress);
		phone = (EditText) findViewById(R.id.etPhone);
		email = (EditText) findViewById(R.id.etEmail);

		save = (Button) findViewById(R.id.btnSave);
		load = (Button) findViewById(R.id.btnLoad);
		clear = (Button) findViewById(R.id.btnClear);

		save.setOnClickListener(new View.OnClickListener() {

			@Override
			public void onClick(View v) {
				try {

					json1.put("name", name.getText().toString());
					json1.put("address", address.getText().toString());
					json1.put("phone", phone.getText().toString());
					json1.put("email", email.getText().toString());

					jsonArray.put(json1);

					json.put("contact", jsonArray);

					serializedJson = json.toString();

					FileOutputStream fos = openFileOutput("contacts.json",
							Context.MODE_PRIVATE);
					byte[] bytesToWrite = serializedJson.getBytes();
					fos.write(bytesToWrite);
					fos.flush();
					fos.close();

					Log.i("", serializedJson);
					Toast.makeText(MainActivity.this, "Saved",
							Toast.LENGTH_LONG).show();

				} catch (JSONException e) {
					// TODO Auto-generated catch block
					e.printStackTrace();
				} catch (FileNotFoundException e) {
					// TODO Auto-generated catch block
					e.printStackTrace();
				} catch (IOException e) {
					// TODO Auto-generated catch block
					e.printStackTrace();
				}

				// Log.i("json", jsonName + jsonAddress + jsonPhone +
				// jsonEmail);
			}
		});

		load.setOnClickListener(new View.OnClickListener() {

			@Override
			public void onClick(View v) {
				Toast.makeText(MainActivity.this, "Loaded", Toast.LENGTH_LONG)
						.show();
				try {

					FileInputStream fis = openFileInput("contacts.json");
					byte[] buffer = new byte[512];
					int bytesRead = fis.read(buffer);
					String textRead = new String(buffer, 0, bytesRead);
					
					JSONObject deserialized = new JSONObject(textRead);
					JSONArray contactArray = deserialized.getJSONArray("contact");

					for (int i = 0; i < contactArray.length(); ++i) {
						JSONObject contact = contactArray.getJSONObject(i);
						name.setText(contact.getString("name"));
						address.setText(contact.getString("address"));
						phone.setText(contact.getString("phone"));
						email.setText(contact.getString("email"));
					}

				} catch (JSONException e) {
					// TODO Auto-generated catch block
					e.printStackTrace();
				} catch (FileNotFoundException e) {
					// TODO Auto-generated catch block
					e.printStackTrace();
				} catch (IOException e) {
					// TODO Auto-generated catch block
					e.printStackTrace();
				}

			}
		});

		clear.setOnClickListener(new View.OnClickListener() {

			@Override
			public void onClick(View v) {
				Toast.makeText(MainActivity.this, "Cleared", Toast.LENGTH_LONG)
						.show();
				name.setText("");
				address.setText("");
				phone.setText("");
				email.setText("");

			}
		});
	}

	@Override
	public boolean onCreateOptionsMenu(Menu menu) {
		// Inflate the menu; this adds items to the action bar if it is present.
		getMenuInflater().inflate(R.menu.main, menu);
		return true;
	}

	@Override
	public boolean onOptionsItemSelected(MenuItem item) {
		// Handle action bar item clicks here. The action bar will
		// automatically handle clicks on the Home/Up button, so long
		// as you specify a parent activity in AndroidManifest.xml.
		int id = item.getItemId();
		if (id == R.id.action_settings) {
			return true;
		}
		return super.onOptionsItemSelected(item);
	}
}
