using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class BlendedPlayerController : MonoBehaviour
{
    Animator animate;
    private Rigidbody rb;
    public float VelocityZ = 0.0f;
    public float VelocityX = 0.0f;
    public float acceleration = 2.0f;
    public float deceleration = 2.0f;
    public float maxWalkSpeed = 0.5f;
    public float maxRunSpeed = 2.0f;
    public float characterMovementSpeed = 3f;
    // Start is called before the first frame update
    void Start()
    {
        
        animate = GetComponent<Animator>();
        rb = GetComponent<Rigidbody>();
    }

    // Update is called once per frame
    void FixedUpdate()
    {
        bool forwardPressed = Input.GetKey(KeyCode.W);
        bool leftPressed = Input.GetKey(KeyCode.A);
        bool rightPressed = Input.GetKey(KeyCode.D);
        bool runPressed = Input.GetKey(KeyCode.LeftShift);
        bool jumpPressed = Input.GetKey(KeyCode.Space);
        //finding the current velocity of the player
        float currentMaxVelocity = runPressed ? maxRunSpeed : maxWalkSpeed;
        //Getting current Axis of player
        float horizontalPosition = Input.GetAxis("Horizontal");
        float verticalPosition = Input.GetAxis("Vertical");
        //for controlling the movement of player
        float currentHorizontalSpeed = (VelocityX < 0.0f) ? -characterMovementSpeed : characterMovementSpeed;
        rb.velocity = new Vector3(horizontalPosition * VelocityX * currentHorizontalSpeed, rb.velocity.y, verticalPosition * VelocityZ * characterMovementSpeed);
        //Statements to Increase the speed gradually
        if(forwardPressed && VelocityZ < currentMaxVelocity){
            VelocityZ += Time.deltaTime * acceleration;
        }
        if(leftPressed && VelocityX > -currentMaxVelocity){
            VelocityX -= Time.deltaTime * acceleration;
        }
        if(rightPressed && VelocityX < currentMaxVelocity){
            VelocityX += Time.deltaTime * acceleration;
        }
        //Statements to decrease the speed
        if(!forwardPressed && VelocityZ > 0.0f){
            VelocityZ -= Time.deltaTime * deceleration;
        }
        if(!rightPressed && VelocityX > 0.0f){
            VelocityX -= Time.deltaTime * deceleration;
        }
        if(!leftPressed && VelocityX < 0.0f){
            VelocityX += Time.deltaTime * deceleration;
        }
        //Resetting of all the variables.
        if(!forwardPressed && VelocityZ <0.0f){
            VelocityZ = 0.0f;
        }
        if(!rightPressed && !leftPressed && VelocityX != 0.0f && (VelocityX > -0.05f && VelocityX < 0.05f)){
            VelocityX = 0.0f;
        }
        if(forwardPressed && runPressed && VelocityZ > currentMaxVelocity){
            VelocityZ = currentMaxVelocity;
        }
        else if(forwardPressed && VelocityZ>currentMaxVelocity){
            VelocityZ -= Time.deltaTime * deceleration;
            if(VelocityZ<currentMaxVelocity && VelocityZ > (currentMaxVelocity - 0.05f)){
                VelocityZ = currentMaxVelocity;
            }
        }
        else if(forwardPressed && VelocityZ < currentMaxVelocity && VelocityZ > (currentMaxVelocity - 0.05f)){
            VelocityZ = currentMaxVelocity;
        }
        if(jumpPressed){
            animate.SetBool("isJumping",true);
        }else{
            animate.SetBool("isJumping", false);
        }
        animate.SetFloat("Velocity Z", VelocityZ);
        animate.SetFloat("Velocity X", VelocityX);
    }
}
