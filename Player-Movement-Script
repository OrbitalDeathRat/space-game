using UnityEngine;
using System.Collections;

public class PlayerMove : MonoBehaviour {
	public float acc = 500.0f;
	public float turnAcc = 50.0f;
	public float pitchAcc = 200.0f;
	public float rollAcc = 100.0f;

	Vector3 playerRot;

	bool addingForce = false;
	// Update is called once per frame
	void Update () {
		playerRot.x = transform.rotation.x;
		playerRot.y = transform.rotation.y;
		playerRot.z = transform.rotation.z;

		//Backwards - forwards velocity.	
		if(Input.GetKey(KeyCode.W)){
			GetComponent<Rigidbody>().AddRelativeForce(0,0,acc*Time.deltaTime);
		}


		if(Input.GetKey(KeyCode.S)){
			GetComponent<Rigidbody>().AddRelativeForce(0,0,-acc*Time.deltaTime);
		}


		// Yaw
		if (Input.GetKey (KeyCode.E)) {
			GetComponent<Rigidbody>().AddRelativeTorque (0, turnAcc *Time.deltaTime, 0);
		}
		if (Input.GetKey (KeyCode.Q)) {
			GetComponent<Rigidbody>().AddRelativeTorque(0, -turnAcc *Time.deltaTime, 0);
		}

		//Pitch
		GetComponent<Rigidbody>().AddRelativeTorque(Input.GetAxis("Mouse Y")*pitchAcc*Time.smoothDeltaTime, 0, 0);


		if(Input.GetKey(KeyCode.A)){
			GetComponent<Rigidbody>().AddRelativeTorque(0,0,rollAcc*Time.deltaTime);
		}
		if(Input.GetKey(KeyCode.D)){
			GetComponent<Rigidbody>().AddRelativeTorque(0,0,-rollAcc*Time.deltaTime);
		}



		Debug.Log (GetComponent<Rigidbody>().velocity.magnitude);
		//clamping
		GetComponent<Rigidbody>().velocity = Vector3.ClampMagnitude (GetComponent<Rigidbody>().velocity, 20.0f);
		GetComponent<Rigidbody>().maxAngularVelocity = 5;

	}
}
